# Installing WezTerm Terminal on macOS

## Foreword

This manual isn't directly related to Nushell, but to make my life as a presenter more convenient and to share my expertise with total beginners, I decided to create this guide.

## Installing WezTerm

Download and install WezTerm from the official page: https://wezterm.org/install/macos.html

Launch WezTerm to verify that it works correctly.

## Configuring WezTerm to Launch Nushell by Default

Open Terminal and execute the following commands:

```nu
# Launch Nushell (if not already in Nushell)
nu

# Navigate to config directory
cd ~/.config/

# Create wezterm directory
mkdir wezterm

# Open wezterm.lua in VS Code
code wezterm.lua
```

In the `wezterm.lua` file that just opened in VS Code, paste the following configuration: 

```lua
-- Load the wezterm module
local wezterm = require 'wezterm'

-- Initialize configuration object
local config = wezterm.config_builder and wezterm.config_builder() or {}

-- Use WebGPU for better performance
config.front_end = "WebGpu"
config.webgpu_power_preference = "HighPerformance"

-- Set Nushell as the default shell
config.default_prog = {'/opt/homebrew/bin/nu'}

-- Get the home directory (works on both macOS and Windows)
local home = os.getenv("HOME") or os.getenv("USERPROFILE") or ""

-- Set XDG_CONFIG_HOME environment variable for Nushell
config.set_environment_variables = {
    XDG_CONFIG_HOME = home .. "/.config",
}

return config
```

> [!NOTE]
> The WebGPU settings ensure WezTerm works properly in various environments, including virtual machines. If you experience issues launching WezTerm on your system, these settings help ensure compatibility.

Save the file in VS Code.

Close and relaunch WezTerm. It should now start with Nushell as the default shell.

## Setting $env.PATH variable

But, mind, that Nushell now doesn't know about the PATH. For example, if we execute `code`, we'll get an error.

Let's fix that. In the Terminal.app, execute the command:

```
    $env.PATH
    | split row (char esep)
    | to nuon --indent 4
```

copy the result. And in your `config.nu` assign the variable `$env.PATH` to the value that we copyied.

## What's Next?

Congratulations! You've successfully installed and configured WezTerm to work with Nushell.

WezTerm is a powerful, GPU-accelerated terminal emulator that offers excellent performance and extensive customization options. With Nushell configured as your default shell in WezTerm, you now have a modern, efficient terminal environment optimized for your Nushell learning journey. As you continue working through these tutorials, feel free to explore WezTerm's additional features and customization options in its documentation.
