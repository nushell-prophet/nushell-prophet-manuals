# Installing Nushell from Scratch on MacOS Tahoe

## Foreword

This manual helps macOS users install Nushell from scratch and set it up properly according to the author's opinion. We'll install Homebrew package manager, set the XDG_CONFIG_HOME environment variable, set up Git version control for tracking your configuration changes, and establish best practices for managing your Nushell environment. By the end, you'll have a solid foundation for learning and using Nushell effectively.

## Installing VS Code

For the tasks in this manual, we'll need a text editor. The manual's author uses `helix editor`, but for beginners (the target audience of this manual), VS Code will be simpler and more reliable at first. We'll install it now. Download the installer from:

https://code.visualstudio.com

## Installing Homebrew

Open https://brew.sh, copy the installation command.
Open Terminal, paste the command, press Enter.

After execution, copy the commands provided by Homebrew (adding to PATH), paste into terminal, execute.

```bash
# Verify the installation
brew doctor
```

## Installing Nushell

```bash
# View package information
brew info nushell

# Install nushell
brew install nushell

# Launch nushell
nu
```

## Preparing to Use XDG_CONFIG_HOME

Check the current configuration path:

```nu
$nu.default-config-dir
```

If the path contains spaces (which it does by default on macOS), follow these instructions to relocate the configuration. This avoids issues when copy-pasting paths, improves compatibility with terminal quick-select features, and provides other convenience benefits that the author has learned from experience.

```nu
# Launch nu without saving history (this prevents recreating the config folder during the move)
nu --no-history

# Create .config directory
mkdir ~/.config

# Move configuration to new location (preserves existing history and settings)
mv $nu.default-config-dir ~/.config/

# Verify that the folder appeared
ls ~/.config/nushell

# Create symbolic link (ensures config is found even when XDG_CONFIG_HOME isn't set)
# The command in parens gets the parent directory of the old config location to create a symlink at
ln -s ~/.config/nushell ($nu.default-config-dir | path dirname)

# Verify that the symbolic link works
ls $nu.default-config-dir
```

Close the terminal tab and open a new tab with zsh (we need to configure the shell that launches Nushell).

## Configuring XDG_CONFIG_HOME

Add the environment variable to zsh configuration (zsh is the default macOS shell, so setting it here ensures it's available when launching Nushell):

```bash
# Open zsh configuration in VS Code
code ~/.zshrc
```

If the `code` command is not found, open VS Code, press `Cmd+Shift+P`, type `install path`, select the install command, press Enter. Then repeat `code ~/.zshrc` in the terminal.

In the opened file, add the line:

`export XDG_CONFIG_HOME="$HOME/.config"`

```bash
# Apply changes
source ~/.zshrc

# Verify that the variable is set
echo $XDG_CONFIG_HOME
```

```nu
# Launch nushell again
nu

# Verify that Nushell is using the new location (should show `~/.config/nushell`)
$nu.default-config-dir
```

## Initializing Git Repository

```bash
# Navigate to configuration directory
cd ~/.config/

# Initialize git
git init

# Add files
git add nushell/config.nu nushell/env.nu

# Create first commit
git commit -m "Initial nushell configuration"

# Set username and email (replace with your own name and email)
git config --global user.name "Maxim Uvarov"
git config --global user.email "nushell-prophet-demo@users.noreply.github.com"

# Edit the author of the last commit
git commit --amend --reset-author
```

## Basic Settings

```nu
# Open environment variables file
config env
```

If the `$env.EDITOR` variable is not set, add to the file:

`$env.EDITOR = "code"`

Save and restart nushell:

```nu
nu

# Open main configuration file
config nu
```

Add history and banner settings:

```nu
$env.config.history.file_format = "sqlite"
$env.config.history.max_size = 5_000_000
$env.config.show_banner = false
```

Save the file.

```nu
# restart nushell
nu

# Import history from txt to sqlite (if you had previous txt-format history)
history import

cd ~/.config/
```

Commit changes:

```nu
# See what changed
git status

# Commit our changes
git add nushell/config.nu nushell/env.nu
git commit -m "first settings"

# Check again
git status
```

We see that history files remain. Create `.gitignore`:

```bash
# Open .gitignore in editor
code .gitignore
```

Add the line: `nushell/history*`

Save and commit:

```nu
# Verify that history files are no longer shown
git status

# Commit .gitignore
git add .gitignore
git commit -m "Add history files to gitignore"
```

## What's Next?

Congratulations! You've successfully set up Nushell with a clean, professional configuration. Your setup now includes:
- A space-free configuration path for smooth workflow
- XDG_CONFIG_HOME properly configured
- Git version control to track and experiment with your configuration safely

You're now ready to start exploring Nushell's powerful features. Don't hesitate to experiment with your configuration - with Git tracking your changes, you can always revert if something doesn't work as expected. Stay tuned for upcoming manuals that will guide you through your Nushell journey. Happy scripting!
