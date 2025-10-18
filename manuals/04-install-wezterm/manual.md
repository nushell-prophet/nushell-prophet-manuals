## Foreword

This manual isn't directly related to Nushell, but to make my life as a presenter more convenient and to share my expertise with total beginners, I decided to create this guide.

## WezTerm installation

Download and install WezTerm from page: https://wezterm.org/install/macos.html

Launch WezTerm to check that it works.

## Making WezTerm to launch with Nushell by default

Launch terminal.

```
nu

cd ~/.config/

mkdir wezterm

code wezterm.lua

```

paste the next code into `wezterm.lua` that was just opened. 

```lua
local wezterm = require 'wezterm'

local config = wezterm.config_builder and wezterm.config_builder() or {}

config.front_end = "WebGpu"
config.webgpu_power_preference = "HighPerformance"
config.default_prog = {'/opt/homebrew/bin/nu'}

local home = os.getenv("HOME") or os.getenv("USERPROFILE") or ""

config.set_environment_variables = {
    XDG_CONFIG_HOME = home .. "/.config",
}

return config
```

Save the file and relaunch WezTerm
