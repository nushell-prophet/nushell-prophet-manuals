Video Narration: Installing New-shell from Scratch on mac-O-S Tahoe

Introduction

This is a tutorial on installing New-shell on mac-O-S.

I'm using a clean mac-O-S Tahoe virtual machine to ensure we cover all setup steps from scratch.

You'll find the link to this manual in the description.

We'll install Homebrew, configure the xdg-config-home environment variable, and set up Git to track your configuration changes. By the end, you'll have a solid foundation for learning and using New-shell effectively.

First, we need a text editor. I personally use the Helix editor, but for beginners, V S Code is simpler and more reliable to start with. I'll head over to code-dot-visualstudio-dot-com and download the installer. After downloading, I'll move the file into the Applications folder, then open V S Code. I'll confirm the security request from mac-O-S since this is the first time opening the app. Now I'll close the unneeded panes in V S Code. We're ready to continue.

Installing Homebrew

Next, let's install Homebrew, the package manager we'll use to install New-shell. I'll open brew-dot-sh in my browser and copy the installation command.

Now I'll open Terminal, paste that command, and press Enter.

After the installation completes, Homebrew will display some commands I need to run. You'll see them in the terminal output—I'll copy those commands, paste them into the terminal, and execute them. This adds Homebrew to the shell's PATH.

Let's verify the installation by running:



If everything looks good, we're ready to move on.

Installing New-shell

Now for the main event—installing New-shell! First, I'll check out the package information:



This shows what version we're about to install. Now I'll install it:



Once that's done, I'll launch New-shell by typing:



And there we go—New-shell is running!

Preparing to Use xdg-config-home

Now let's check where New-shell stores its configuration. I'll run:



You'll notice the path contains spaces—this is the default on mac-O-S. From my experience, having spaces in config paths causes issues when copy-pasting, doesn't work well with terminal quick-select features, and creates other inconveniences. So let's relocate the configuration to a better location.

First, I'll launch New-shell without saving history—this prevents recreating the config folder during the move:



Now I'll create the dot-config directory:



I'll move the configuration to the new location. This preserves existing history and settings:



Let's verify the folder appeared:



Good! Now I'll create a symbolic link. This ensures the config is found even when xdg-config-home isn't set:



Let's verify the symbolic link works:



Perfect! Now I'll exit this session of New-shell back to zsh—we need to configure the shell that launches New-shell.

Configuring xdg-config-home

Since zsh is the default mac-O-S shell, I'll add the xdg-config-home environment variable to its configuration. This ensures it's available when launching New-shell.

I'll try to open the zsh configuration file in V S Code with command `code`. And as we just installed the editor, the command isn't available in our environment yet.


To fix the "command not found" error, I'll open V S Code, press Command-Shift-P, type "install path", select the install command, and press Enter. I'll confirm the action in the mac-O-S popup by entering my password. Then I'll try the code command again.

And now it works. In the file I'll add this line:



I'll save the file. In the video, I exit from New-shell to zsh, and then I apply the changes:



I'll verify the variable is set:



You should see the path printed. I'll close the file in V S Code now.

Now I'll launch New-shell again:



And I'll verify New-shell is using the new location:



You should see tilde-slash-dot-config-slash-nushell—a path without spaces. Excellent!

Initializing Git Repository

Now let's set up Git to track the configuration changes. This is really helpful—if something gets messed up, it's easy to revert to a working state.

I'll navigate to the config directory:



First, I'll configure Git with my name and email. You should replace these with your own:



I'll initialize the Git repository:



Let's check what's in the current directory—only the nushell folder in my case. Now I'll check what's inside the nushell folder.

I'll add the New-shell configuration files:



And create the first commit:



Let's verify the commit by running git log.

Great! The configuration is now tracked by Git.

Basic Settings

Let's configure some basic settings. First, I'll open the environment variables file:



If this doesn't work, it's because the EDITOR environment variable isn't set (as you can see in the error message). I'll set it by running:



Then I'll run config env again. The default env-dot-nu file provided by New-shell should open in V S Code. You can see it has helpful comments and examples. I'll add that same line to the end of the file to make it persistent, then save.

Now I'll restart New-shell:



Now, because of the changes we made, I can open the main configuration file with this command:



I'll confirm the requests from V S Code to trust the workspace and to use the Git repository for the folder where our files are located.

Now I'll install the New-shell language extension for V S Code. I'll open the extensions section, search for "nushell", click Install, and confirm that I trust the authors of the extension.

With the extension installed, you can see that the comments in our config-dot-nu file are now highlighted in green.

Next, I'll execute the command from the comments to see all the settings that are available for New-shell. I'll pick the most important ones for now.

To move up and down by one line, I use the j and k keys. To enter search mode, I press the slash key, type "banner", hit Enter, and copy the line found.

However, in my settings I'll change the value from true to false.

You can find these exact settings in the manual—they switch the history to S-Q-L-ite format for storing additional meta information, increase the history database table size, and disable the startup banner.

I'll save the file and restart New-shell:



To preserve my text-based history, I'll import it to S-Q-L-ite:



I'll navigate back to the config directory:



Now let's commit these changes. First, I'll see what changed:



I'll commit the changes:



I'll check the status again:



You'll notice history files showing up. We don't want to track those in Git, so I'll create a dot-gitignore file:



I'll add this line:



I'll save the file. Now I'll check the status:



The history files should no longer appear. Now I'll commit the dot-gitignore file using the commands from the manual.



Perfect!

Conclusion

Congratulations! We've successfully set up New-shell with a clean, solid foundation to build on.

We're now ready to start exploring New-shell's powerful features. Don't hesitate to experiment with the configuration—with Git tracking changes, you can always revert if something doesn't work as expected.

Stay tuned for upcoming manuals that will guide you through your New-shell journey. Happy scripting, and I'll see you in the next video!
