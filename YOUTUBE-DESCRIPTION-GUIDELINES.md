# YouTube Description Guidelines

This document provides guidelines for creating YouTube video descriptions for manual tutorials in this repository.

## File Location

Each manual should have its YouTube description stored in:
```
manuals/NN-descriptive-name/youtube-description.md
```

## Structure

A YouTube description should include the following elements:

### 1. Opening Hook (Required)
Start with a compelling 1-2 sentence introduction that:
- Clearly states what the video covers
- Indicates the target audience (e.g., "Perfect for beginners")
- Highlights the value proposition

Example:
```
Learn how to install and set up Nushell on macOS with this comprehensive
step-by-step tutorial! Perfect for beginners who want to get started with
this modern, powerful shell.
```

### 2. What You'll Learn Section (Recommended)
Use the 🔧 emoji followed by "What You'll Learn:" and bullet points listing:
- Main topics covered
- Key skills or knowledge gained
- Important configuration steps

Example:
```
🔧 What You'll Learn:
- Installing VS Code text editor
- Setting up Homebrew package manager
- Installing Nushell via Homebrew
```

### 3. Prerequisites Section (If Applicable)
Use the 📝 emoji followed by "Prerequisites:" and list:
- Required OS/software versions
- Prior knowledge needed (or state "No prior X experience needed!")
- Hardware requirements if relevant

### 4. Why/Context Section (Optional)
Use the 💡 emoji to provide context:
- Explain the reasoning behind certain choices
- Highlight best practices being followed
- Provide additional motivation for viewers

### 5. Call-to-Action (Required)
Include standard engagement prompts:
```
👍 Like this video if you found it helpful!
🔔 Subscribe for more Nushell tutorials and shell scripting content!
💬 Questions? Drop them in the comments below!
```

### 6. Links Section (Required)
Include:
- Link to the full manual on GitHub using the 📖 emoji
- Any external resources mentioned in the video
- Related videos or playlists (if applicable)

Example:
```
📖 Full manual: https://github.com/nushell-prophet/nushell-prophet-manuals/blob/main/manuals/01-install-nushell-macos/manual.md
```

### 7. Hashtags (Required)
End with relevant hashtags (typically 5-8):
- Include #nushell for all Nushell-related content
- Add platform tags (#macos, #linux, etc.)
- Include topic tags (#terminal, #shell, #tutorial, #programming)
- Add specific tool tags when relevant (#claudecode, #ai, etc.)

## Style Guidelines

### Tone
- Friendly and approachable
- Clear and direct
- Encouraging for beginners
- Professional but not overly formal

### Formatting
- Use emojis strategically for visual scanning (don't overuse)
- Break content into clear sections
- Use bullet points for lists
- Keep paragraphs short and readable

### Language
- Write in clear, simple English
- Avoid jargon unless necessary (and explain when used)
- Use active voice
- Be specific rather than vague

### Length
- Aim for 150-300 words (before links and hashtags)
- Include enough detail to be informative
- Keep it concise enough that viewers will read it

## Variations by Content Type

### Installation/Setup Tutorials
Focus on:
- Clear step-by-step overview
- Prerequisites
- What gets installed/configured
- Why certain choices are made

### Feature/Usage Tutorials
Focus on:
- What problem it solves
- Key features demonstrated
- Practical use cases
- Tips and best practices

### Troubleshooting/Tips Videos
Focus on:
- The problem being solved
- Who this helps
- Quick preview of the solution
- Related issues covered

## Examples

See these manuals for reference:
- `manuals/01-install-nushell-macos/youtube-description.md` - Comprehensive installation tutorial
- `manuals/02-install-claude-code-macos/youtube-description.md` - Tool installation with context

## Checklist

Before publishing, verify:
- [ ] Opening hook is compelling and clear
- [ ] All relevant sections are included
- [ ] Link to GitHub manual is correct and uses main branch
- [ ] External links are working
- [ ] Hashtags are relevant
- [ ] Grammar and spelling are correct
- [ ] Emojis are used consistently
- [ ] Call-to-action is included
- [ ] Description is 150-300 words (optimal for YouTube SEO)
