---
youtube:
telegram:
---

# Installing Cozy into an `sbx` Sandbox

## Foreword

Cozy is the terminal environment I use to work with AI agents inside isolated sandboxes. It bundles Nushell, Zellij, Helix, lazygit, broot, topiary, Claude Code with a Nushell MCP server, and a set of custom Nushell modules — all set up in one command. In the [first video](https://youtu.be/AcDM7-U2e2A) I showed cozy in action. This manual is the install: we set cozy up from scratch and look at what actually happens during the install.

## Prerequisite: the `sbx` CLI

Cozy's primary target is `sbx` — Docker's standalone sandbox runtime. It creates isolated Linux virtual machines where you work with AI agents. So the only prerequisite is the `sbx` CLI itself. The install steps are in Docker's docs: https://docs.docker.com/ai/sandboxes/#get-started

If you don't use `sbx` at all, cozy still installs on a plain host or into a container — see [Installing without sbx](#installing-without-sbx) at the end.

## The three-command quick start

```sh
git clone https://github.com/nushell-prophet/cozy
cd cozy

# Create the sandbox. `shell` is the agent (Docker's standard sandbox image);
# `--kit sbx-kit/` layers cozy on top. The trailing folders are host dirs
# mounted into the sandbox as the workspace — the first one is where you start.
sbx create --name NAME --kit sbx-kit/ shell ~/some/dir ~/another/dir

# Connect once the install is done.
sbx exec -it NAME nu --login --execute 'zellij attach -c NAME'
```

The rest of this manual unpacks these three commands and shows what the installer does in between.

## Unpacking `sbx create`

- `--name NAME` names the sandbox. Pick anything; you use it again in the connect command and in `sbx ls`.
- `shell` is the agent — the standard sandbox image from Docker.
- `--kit sbx-kit/` layers cozy on top. A kit is a small spec file that says what to run inside the sandbox after it is created.
- The last arguments are folders from your machine that get mounted into the sandbox as the workspace. The first one is where you start.

One thing to note: the kit installs cozy from GitHub — the latest commit on the default branch — not from your local checkout. The clone is only needed for the kit file ([`sbx-kit/spec.yaml`](https://github.com/nushell-prophet/cozy/blob/master/sbx-kit/spec.yaml)) and the WezTerm config later. Push your changes before `sbx create`, or pin `--branch <tag>` on the clone line in `sbx-kit/spec.yaml` if you need a reproducible install.

## Watching the install log

While `sbx create` runs it looks completely silent — `sbx` swallows the install output. But the installer writes everything to a log file, so from a second terminal you can watch the progress:

```sh
sbx exec -it NAME tail -f /home/agent/cozy-install.log
```

Here `sbx exec -it` opens an interactive shell in the sandbox, and `tail -f` follows the log as it grows.

## What the installer does

You don't run any of the steps below by hand — `sbx create` runs them for you. This section explains what lands in the sandbox, so nothing is a black box.

### The kit file — [`sbx-kit/spec.yaml`](https://github.com/nushell-prophet/cozy/blob/master/sbx-kit/spec.yaml)

The kit is one small file. It does three things:

- **Environment variables** — mirrors the ENV of the cozy Docker image (PATH, the XDG dirs, `HELIX_RUNTIME`, the Homebrew no-prompt flags).
- **Network allowlist** — the only domains the install may reach: Homebrew, GitHub, the apt mirrors, and claude.ai. Nothing else.
- **Two commands** — first, a shallow clone of cozy into the sandbox (latest default branch); second, `run-install.sh`, with its output redirected into the log you are tailing.

### [`run-install.sh`](https://github.com/nushell-prophet/cozy/blob/master/cozy-module/install/run-install.sh)

Everything interesting lives in one script — the same one a plain host install and the Docker build run, so the three paths can't drift apart. It makes sure Homebrew is present: in the sandbox (Linux, passwordless sudo) it installs brew automatically; on a real host it stops and shows you the command, so your sudo password never goes through a script. Then a small helper ([`ensure-nu.sh`](https://github.com/nushell-prophet/cozy/blob/master/cozy-module/install/ensure-nu.sh)) picks a Nushell able to run the installer — pinning a known-good version if brew's is too new. The real work is in `bootstrap.nu`, the main installer, itself written in Nushell.

### [`bootstrap.nu`](https://github.com/nushell-prophet/cozy/blob/master/cozy-module/install/bootstrap.nu) — the install plan

Every step that turns a bare sandbox into cozy:

0. **Container setup** — rewrite the apt sources to HTTPS, install a few apt build deps (`gcc`, `libc6-dev`, `procps`, `file`), and write the runtime env exports the sandbox shell sources on each login. The [`pbcopy` shim](https://github.com/nushell-prophet/cozy/blob/master/docker-files/pbcopy) (OSC 52 clipboard) is installed on every Linux.
1. **brew tools** — `nushell fzf lazygit helix zellij broot git-delta visidata bat topiary fd jj git-lfs`.
2. **Git config** — a minimal XDG git config with an agent identity, because the installer itself needs to commit. Your own `~/.gitconfig` still wins over it.
3. **Vendored modules** — the bundled Nushell modules fan out into `~/repos/`, straight from the committed `vendor/` snapshot, so no extra fetches.
4. **Autoload scripts** — the scripts that load the modules on every shell start. The dir is wiped first, so a file removed upstream doesn't linger.
5. **Dotfiles and skills** — the dotfiles are deployed and the Claude Code skills installed.
6. **Global Claude instructions** — the tool catalog is appended to `~/.claude/CLAUDE.md`.
7. **broot** — gets its default config.
8. **topiary** — the tree-sitter-nu grammar, compiled locally, so Nushell code can be formatted.
9. **Claude Code + MCP** — Claude Code is installed and the Nushell MCP server registered, so the agent gets a persistent Nushell session out of the box.

The very last write is a small stamp file (`~/.cozy-installed`) — last on purpose: a failed install leaves no stamp, so nothing pretends to be complete.

## Connecting to the sandbox

When the log says the install is done, the third command connects:

```sh
sbx exec -it NAME nu --login --execute 'zellij attach -c NAME'
```

Here `nu --login --execute` starts a Nushell login shell inside the sandbox and runs one command — `zellij attach -c NAME` — which attaches to the Zellij session, creating it on the first run.

### Connecting through WezTerm (recommended on macOS)

On my Mac I connect through WezTerm — one command opens a window straight into the sandbox, with the QuickSelect patterns and keybindings from the first video. The config it loads ([`vendor/dotfiles/wezterm/wezterm.lua`](https://github.com/nushell-prophet/cozy/blob/master/vendor/dotfiles/wezterm/wezterm.lua)) is vendored in the cozy repo:

```sh
# NAME = your sandbox name (from `sbx ls`) — replace all three.
wezterm --config-file vendor/dotfiles/wezterm/wezterm.lua --config 'colors={background="#000000"}' start -- sbx exec -it NAME nu --login --execute 'zellij attach -c NAME'
```

Install WezTerm with `brew install wezterm --cask`. See also [manual 04](../04-install-wezterm/manual.md).

WezTerm is more than cosmetic here — it is a substantial part of the setup. A terminal normally claims shortcuts like Cmd+T and Cmd+W for its own tabs and windows, so they never reach what runs inside it. The cozy config disables all of WezTerm's default keybindings, so those familiar shortcuts pass through to Zellij and the apps behind it (forwarded as kitty-protocol escape sequences) instead of the terminal window. That is what lets Zellij own the tab and pane shortcuts inside the sandbox.

> [!IMPORTANT]
> If you use a different terminal — or skip WezTerm — free up its default keybindings the same way, or the terminal will swallow the shortcuts Zellij expects. Every terminal has its own way to do this; check its docs for disabling default shortcuts. On any terminal you can also run `cozy swap-zellij-super` inside the sandbox to move Zellij's bindings from Super (Cmd) to Alt, which sidesteps most clashes.

## Verify: `cozy verify`

To check that everything landed, cozy ships its own check ([`cozy-module/verify.nu`](https://github.com/nushell-prophet/cozy/blob/master/cozy-module/verify.nu)). Inside the sandbox, run:

```sh
cozy verify
```

It goes through the environment and reports what works.

## Windows note

On Windows the Cmd key doesn't exist, and Win-key combinations are reserved by the OS. So run this inside the sandbox to remap the Zellij bindings from Super to Alt ([`cozy-module/swap-zellij-super.nu`](https://github.com/nushell-prophet/cozy/blob/master/cozy-module/swap-zellij-super.nu)):

```sh
cozy swap-zellij-super
```

## Installing without sbx

If you don't use `sbx` at all, the same `run-install.sh` installs the same toolset on a plain host or into a container — on a host the only prerequisite is Homebrew. There is also a Debian image for plain `docker run`, still in testing. See the cozy README's [*Install elsewhere*](https://github.com/nushell-prophet/cozy#install-elsewhere) section for details.
