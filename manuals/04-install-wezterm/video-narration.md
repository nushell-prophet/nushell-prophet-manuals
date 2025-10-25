In this video we will install WezTerm terminal and make it launch New-shell by default.

This video has an accompanying manual. I'll open it, and I'll be copying commands from this manual throughout the video.

Let's download the WezTerm app from the official site and move it to our Applications folder.

Next, let's launch the standard Terminal app.

I'll launch New-shell and navigate to the dot-config directory.

Now I'll create a wezterm directory and navigate to it.

Now I'll run the code command to open wezterm-dot-lua in V S Code. Since this file doesn't exist yet, V S Code will create a new empty file with this name.

Now we're ready to fill this file with settings from our manual. For demonstration purposes, I'll add the settings in chunks to show you the differences they make, but you can just copy the complete settings all at once.

The first settings improve WezTerm's performance. They shouldn't be obligatory for you, but WezTerm refuses to start in my virtual machine without these settings, so I've included them in our manual.

Now I'll launch WezTerm only with these performance settings, leaving other settings at their defaults. This will show that WezTerm launches the default zsh shell with the same configs that are used in the Terminal app.

For example, we can launch New-shell and check that the xdg-config-home variable from the dot-zshrc file that we configured in our previous video is set correctly. 

I'll exit WezTerm to demonstrate the impact of setting the default_prog setting. You can find the value for this variable in a working terminal by running the which nu command.

Now let's launch WezTerm with the current state of configs.

You can notice that New-shell is now launched by default. For example, I can execute the version command straight away and see the colorful New-shell output.

However, if I check the xdg-config-home variable, we'll see that it's not set. New-shell also doesn't know about the existence of code and brew applications in our system.

Let's fix these problems one by one. First, let's set the xdg-config-home variable that default_prog should be launched with.

The highlighted code should work on mac-O-S, Linux, and Windows.

I'll relaunch New-shell to check that the environment variable is now set. Here I'll demonstrate another aspect of the missing PATH configuration: executing config nu will try to call the code app that we previously set in our env-dot-nu file. However, since we haven't included the full path to the application but only used its name, New-shell won't be able to open V S Code with our config.

To proceed with our next step, I'll quit WezTerm and open the Terminal app (where the environment variable editor is already set correctly). I'll execute the "config nu" command there.

In V S Code, I'll exit Restricted mode to allow the New-shell-lang extension to highlight our config-dot-nu file. Then I'll copy the example chunk of code from our manual and paste it into our config-dot-nu file.

In the copied code, I need to replace the list with paths that exist on my machine. To get that list, I'll execute another command from the manual in the Terminal app, as you can see in the video.

I'll copy the output of the command, paste it into V S Code, reindent it, save the file, and launch WezTerm again.

Just as a test, I'll execute the brew doctor command and verify that it works. Don't worry about the warning from Homebrew that I have now. It just says that apps from slash-usr-slash-bin might be used instead of those installed by Homebrew. To get rid of this warning, we could use the prepend command instead of append here in our config.

In the next part of the video, I'll commit the changes that we made without explaining each command. Thanks for watching, and stay tuned!
