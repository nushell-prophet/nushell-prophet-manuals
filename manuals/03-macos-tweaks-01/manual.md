## Foreword

This manual isn't directly related to Nushell, but to make my life as a presenter more convenient and to share my expertise with total beginners, I decided to create this guide.

## Terminal Settings

1. Enable "Close tab with clean exit"
2. Set "Use `Option` as `Meta` key"

## macOS Settings Through Terminal

These terminal commands help optimize your macOS environment ([original source](https://github.com/nushell-prophet/my-dotfiles/blob/master/macos-fresh/useful-settings.nu)):

```bash
# Remove all dock icons
defaults write com.apple.dock persistent-apps -array

# Set key repeat interval
defaults write -g KeyRepeat -int 1 # normal minimum is 2 (30 ms)

# Set initial key repeat delay
defaults write -g InitialKeyRepeat -int 20 # normal minimum is 15 (225 ms)
```

## Finder Settings

- Switch to "as List" view representation everywhere
- Set Dock position on screen to left or right (not bottom)
- Set "Prefer tabs when opening documents" to "Always"
