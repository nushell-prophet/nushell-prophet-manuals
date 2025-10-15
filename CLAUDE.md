# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a documentation repository containing Nushell manuals and tutorials for the [@nushell-prophet YouTube channel](https://www.youtube.com/@nushell-prophet). The content is educational material aimed at helping users learn Nushell, a modern shell written in Rust.

### Channel Mission

The channel focuses on:
- **Documenting practical Nushell use cases** and showcasing terminal workflows
- **Step-by-step beginner manuals** that follow a sequential learning path
- **Related terminal tools** (wezterm, zellij, lazygit, Claude Code, etc.) to help beginners reproduce a complete development environment
- **Advanced content** for experienced users interested in exploring Nushell capabilities

### Content Structure

- **Numbered manuals** (01, 02, 03, etc.) are designed for absolute beginners and follow a sequential learning path
- **Other videos/tutorials** target users already familiar with Nushell or those interested in specific advanced topics
- **Setup/prerequisite content** (macOS configuration, terminal tools) ensures beginners can replicate the environment and follow along with Nushell tutorials

## Structure

- **manuals/** - Contains numbered tutorial manuals, each in its own subdirectory
  - Each manual lives in a folder like `01-install-nushell-macos/`
  - The actual content is in `manual.md` within each folder
  - YouTube descriptions are stored in `youtube-description.md` within each folder
  - Some manuals may include `video-narration.md` for video scripts
- **README.md** - Table of contents listing all available manuals with bullet-point summaries
- **YOUTUBE-DESCRIPTION-GUIDELINES.md** - Guidelines for creating YouTube video descriptions

## Content Guidelines

### Manual Organization

Each manual should:
- Be placed in `manuals/NN-descriptive-name/manual.md` format (where NN is a zero-padded number)
- Have clear section headings that match the structure outlined in README.md
- Target beginners as the primary audience
- Include practical, step-by-step instructions with code examples
- Use markdown code blocks with appropriate language tags (`bash`, `nu`, etc.)

### README Maintenance

When adding or modifying manuals:
- Update README.md to reflect all major sections of the manual
- Use bullet points to list the main sections covered
- Ensure the link path matches the actual manual location
- Keep section names consistent between README and manual headings

### Writing Style

- Focus on practical instructions over theory
- Assume readers are beginners unless stated otherwise
- Use clear, concise language
- Include "What's Next?" sections to guide readers forward
- Avoid unnecessary complexity or advanced configurations for beginner content

### Language and Editing

The author is a non-native English speaker. When reviewing or editing content:
- Proactively check for grammar, spelling, and clarity issues
- Rephrase awkward or unclear sentences while preserving the author's intent
- Suggest improvements to make technical content more accessible
- Fix articles (a/an/the), prepositions, and verb tense issues common to non-native speakers

### YouTube Descriptions

Each manual that has an accompanying video should include a YouTube description:
- Store in `youtube-description.md` within the manual's folder
- Follow the guidelines in `YOUTUBE-DESCRIPTION-GUIDELINES.md`
- Place the full manual link immediately after the opening hook
- Mention the manual link in the opening hook text
- Do not include external links - all resources should be in the manual itself
- Use emojis strategically for visual scanning
- Include relevant hashtags for discoverability
- Keep descriptions 150-300 words for optimal YouTube SEO

## License

This repository uses the Unlicense (public domain).
