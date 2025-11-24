# Prophet's Guide to Nushell

Learn Nushell and set up Prophet's environment (WezTerm, Zellij, Helix, Claude Code)

## About These Manuals

The best place to start learning Nushell is the official [Nushell Book](https://www.nushell.sh/book/)—it's exceptionally well-written, actively maintained, and always up to date.

These manuals serve a different purpose. Unlike the comprehensive Nushell Book, we focus on practical, platform-specific guidance (currently macOS). We start with installation and setup, then progress to tuning Nushell, demonstrating its use for real work tasks, and showcasing other handy CLI and TUI tools. Each manual includes accompanying video guides and provides detailed, step-by-step instructions for newcomers ("nu-bies") who may find certain setup tasks intimidating.

While many configuration steps seem obvious to experienced developers, they can be confusing for beginners. That's why we walk you through each step clearly, providing battle-tested, efficient defaults—though opinionated—so you can get Nushell properly set up and start learning through hands-on experimentation.

## Manuals

1. [Install Nushell on macOS Tahoe from scratch](manuals/01-install-nushell-macos/manual.md)
    - Install VS Code
    - Install Homebrew
    - Install Nushell
    - Prepare to Use XDG_CONFIG_HOME
    - Configure XDG_CONFIG_HOME
    - Initialize Git Repository
    - Basic Settings

2. [Install Claude Code on macOS](manuals/02-install-claude-code-macos/manual.md) *(Optional)*
    - Installing Node.js
    - Installing Claude Code
    - Verifying installation with `/doctor`
    - Installing VS Code extension

2a. [macOS & Terminal Security Awareness](manuals/02a-macos-terminal-security/manual.md) *(Highly Recommended)*
    - Understanding macOS Security (SIP, Gatekeeper, Sandboxing)
    - Software Installation Risks and Trust-Based Distribution
    - Security Red Flags to Avoid Entirely
    - Good Security Habits for Developers
    - Nushell's Security Advantages

2b. [AI Coding Assistants in the Terminal: Understanding the Risks](manuals/02b-ai-coding-assistants-security/manual.md) *(For AI Tool Users)*
    - What Are AI Coding Assistants and Why They're Different
    - The Security Hierarchy: Which Tools to Trust
    - What AI Tools Can Access
    - Risk Assessment Framework
    - Practical Security Measures
    - When to Avoid AI Tools Entirely

3. [macOS Tweaks for Terminal Users](manuals/03-macos-tweaks-01/manual.md)
    - Terminal Settings
    - macOS Settings Through Terminal
    - Finder Settings

4. [Installing WezTerm Terminal on macOS](manuals/04-install-wezterm/manual.md)
    - Installing WezTerm
    - Configuring WezTerm to Launch Nushell by Default
    - Setting the $env.PATH Variable

5. [Setting Up Quick Select Patterns in WezTerm](manuals/05-setup-quick-select-patterns-in-wezterm/manual.md)
    - What Are Quick Select Patterns?
    - Configuring Quick Select Patterns
    - Using Quick Select
