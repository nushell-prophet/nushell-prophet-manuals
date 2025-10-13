## Foreword

> [!NOTE]
> **This manual is completely optional.** If you don't have a Claude subscription, prefer not to use Claude Code, or have any other reason for skipping it, feel free to move on to the next manual. All the other tutorials in this series work perfectly fine without Claude Code. This tool is simply offered as an optional learning aid for those who want to use it.

I love Claude Code, and I believe it has huge potential for teaching users how to use the terminal and for troubleshooting problems that might occur along the way.

Because of that, I decided it might be valuable for some users who have a subscription to Claude to include this manual on installing the Claude Code CLI in a series of Nushell-related manuals.

## Installing Node.js

To install Claude Code, you need to install Node.js first.

You can find instructions on doing so at https://nodejs.org/en/download.

Be aware that after executing the first step provided in the version of instructions from 2025-10-13:

```
# Download and install nvm:
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
```

The installation will display a message telling you to close and reopen your terminal. However, in my case, even after restarting the terminal, `nvm` wasn't available yet. I needed to manually run the export commands shown at the bottom of the installation output (highlighted in the screenshot below).

![](media/nvm-preparations.png)

After running those export commands in the new terminal session, `nvm` became available and I could proceed with the next step.

```
nvm install 22
```

## Installing Claude Code

After installing nvm and checking its functionality, I executed the installation command from the [Claude Code documentation guide](https://docs.claude.com/en/docs/claude-code/setup).

After the installation, I created a test project directory to launch `claude code` from there. It's important to run Claude Code from a project directory rather than from your home directory, as it's designed to work within the context of a specific project.

```
# Create a directory structure for projects
mkdir ~/git
mkdir ~/git/tests

# Navigate to the test directory
cd ~/git/tests/

# Launch Claude Code
claude code
```

In `claude code`, I checked the installation correctness with the command `/doctor`.

Also, in the video, I installed the `claude code` extension for `VS Code`.

## What's Next?

Congratulations! You've successfully installed Claude Code and verified that it's working correctly.

You're now ready to start using Claude Code as your learning companion! As you work through these Nushell tutorials and explore the terminal, Claude Code can help explain commands, troubleshoot errors, and answer questions along the way. Having this AI assistant available from the start will enhance your learning experience and help you understand concepts more quickly. Don't hesitate to ask it questions as you learn - that's exactly what it's there for.

Happy learning!
