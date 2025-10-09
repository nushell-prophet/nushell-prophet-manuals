# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a documentation repository containing Nushell manuals and tutorials. The content is educational material aimed at helping users learn Nushell, a modern shell written in Rust.

## Structure

- **manuals/** - Contains numbered tutorial manuals, each in its own subdirectory
  - Each manual lives in a folder like `01-install-nushell-macos/`
  - The actual content is in `manual.md` within each folder
- **README.md** - Table of contents listing all available manuals with bullet-point summaries

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

## License

This repository uses the Unlicense (public domain).
