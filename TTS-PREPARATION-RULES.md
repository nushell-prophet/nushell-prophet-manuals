# TTS (Text-to-Speech) Preparation Rules

This document contains rules for preparing video narration text for TTS engines to ensure proper pronunciation and natural-sounding output.

## 1. Product and Technology Names

### Replace with phonetic spelling:
- `Nushell` → `New-shell` (to get the correct "oo" sound like in "too")
- `macOS` → `mac-O-S`
- `VS Code` → `V S Code` (with spaces between letters)
- `SQLite` → `S-Q-L-ite`
- `Homebrew` → `Homebrew` (keep capitalized - it's a product name)

### Extension names follow the same pattern:
- `nushell-lang` extension → `New-shell-lang` (VS Code extension)

### Application names:
- `Terminal.app` → `Terminal app` (when referring to the macOS Terminal application in prose)

## 2. URLs and Domains

### Convert to phonetic pronunciation:
- `github.com` → `github-dot-com`
- `brew.sh` → `brew-dot-sh`
- `code.visualstudio.com` → `code-dot-visualstudio-dot-com`
- Pattern: Replace `.` with `-dot-` and `/` with `-slash-`

## 3. Email Addresses

### Spell out special characters:
- `user@example.com` → `user at example dot com`
- Pattern: Replace `@` with ` at ` and `.` with ` dot `

## 4. File Names and Extensions

### Make extensions pronounceable:
- `.config` → `dot-config`
- `env.nu` → `env-dot-nu`
- `config.nu` → `config-dot-nu`
- `.gitignore` → `dot-gitignore`
- `.zshrc` → `dot-zshrc`
- `wezterm.lua` → `wezterm-dot-lua`

## 5. File Paths

### Spell out path components:
- `~/.config/nushell` → `tilde-slash-dot-config-slash-nushell`
- `~/` → `tilde slash`

## 6. Command-Line Flags and Options

### Convert flags to words:
- `--flag` → `minus minus flag`
- `-s` → `minus s`
- `--no-history` → `minus minus no minus history`
- `--global` → `minus minus global`
- `-m` → `minus m`

## 7. Shell Variables and Special Characters

### Dollar signs:
- `$variable` → `dollar variable`
- `$nu.default-config-dir` → `dollar nu dot default minus config minus dir`
- `$HOME` → `dollar HOME`
- `$XDG_CONFIG_HOME` → `dollar XDG_CONFIG_HOME`
- `$env.EDITOR` → `dollar env dot EDITOR`

### Other special characters in commands:
- `=` → `equals`
- `"` → `quote`
- `(` → `open paren`
- `)` → `close paren`
- `|` → `pipe`

### Tildes:
- `~` → `tilde`
- `~/` → `tilde slash`

## 8. Markdown Syntax

### Remove all markdown formatting:
- **Remove heading markers**: `#` and `##` (TTS engines pronounce them as "hash")
- **Remove code blocks**: Remove all ``` markers
- **Keep section titles**: As plain text without any markdown
- **Keep commands**: As plain text, naturally indented
- **Remove inline code backticks**: From prose text (but describe the code phonetically)

## 9. Inline Code References

### Remove backticks and spell out:
- `` `git log` `` → `git log` (plain text)
- `` `j` `` → `j` (plain text)
- `` `k` `` → `k` (plain text)
- `` `true` `` → `true` (plain text)
- `` `false` `` → `false` (plain text)

## 10. Environment Variables

### In prose (lowercase with hyphens for readability):
- `XDG_CONFIG_HOME` → `xdg-config-home` (when mentioned in regular text)
- Keep uppercase in actual commands: `dollar XDG_CONFIG_HOME`

## 11. Complex Command Examples

### Example transformation:
**Before:**
```bash
ln -s ~/.config/nushell ($nu.default-config-dir | path dirname)
```

**After:**
```
ln minus s tilde slash dot config slash nushell open paren dollar nu dot default minus config minus dir pipe path dirname close paren
```

### Example with git:
**Before:**
```bash
git config --global user.email "user@example.com"
```

**After:**
```
git config minus minus global user dot email quote user at example dot com quote
```

### Example with export:
**Before:**
```bash
export XDG_CONFIG_HOME="$HOME/.config"
```

**After:**
```
export XDG_CONFIG_HOME equals quote dollar HOME slash dot config quote
```

## 12. General Guidelines

1. **Test the output**: Always test TTS output to catch any mispronunciations
2. **Be consistent**: Use the same phonetic spelling throughout the document
3. **Readability balance**: While optimizing for TTS, keep the text somewhat readable for humans who might review it
4. **Hyphens for compound words**: Use hyphens to connect words that should be pronounced together (e.g., `brew-dot-sh`)
5. **Spaces for separate words**: Use spaces when each word should be pronounced separately (e.g., `V S Code`)

## 13. What NOT to Change

- Regular prose text (sentences, paragraphs)
- Common programming terms that TTS handles well (Git, Terminal, PATH, EDITOR)
- Numbers (usually pronounced correctly)
- Regular words and punctuation in sentences

## 14. File Structure

For video narration files:
- Remove all markdown headings (`#`, `##`)
- Remove all code block markers (```)
- Keep section titles as plain text
- Keep commands as plain text (no special formatting)
- Apply all phonetic transformations from rules above

## 15. Narration Style Conventions

### Consistency in writing:
- Use contractions consistently: prefer `I'll` over mixing `I will` and `I'll`
- Avoid starting sentences with `And` - use `Now`, `Then`, `Next` instead
- Use proper articles: `the`, `a`, `an` where appropriate
- Distinguish `its` (possessive) from `it's` (contraction of "it is")

### Natural phrasing:
- `Just for test` → `Just as a test` (correct idiom)
- `Nevermind` → `Don't worry about` (more conversational)
- `we might use` → `we could use` (more natural)
- `as you see this` → `as you can see` (standard phrasing)

### Clarity:
- Use Oxford comma in lists of three or more items for clarity
- Example: `copy, paste, and save` (not `copy, paste and save`)

## Quick Reference Checklist

Before finalizing TTS narration text, verify:
- [ ] All URLs converted to phonetic spelling
- [ ] All email addresses use "at" and "dot"
- [ ] All file extensions use "dot-" prefix
- [ ] All command flags use "minus" or "minus minus"
- [ ] All dollar signs replaced with "dollar"
- [ ] All tildes replaced with "tilde"
- [ ] All markdown syntax removed
- [ ] All special characters spelled out in commands
- [ ] Product names (Nushell, macOS, VS Code, SQLite, Homebrew) converted
- [ ] Extension names (nushell-lang → New-shell-lang) converted
- [ ] File paths fully spelled out with slash separators
- [ ] Quotes removed from around commands in narration
- [ ] Contractions used consistently (I'll, we'll, etc.)
- [ ] Oxford commas used for clarity
- [ ] Articles (the, a, an) used properly

## Testing

After applying these rules:
1. Run the text through your TTS engine
2. Listen for any awkward pronunciations
3. Adjust phonetic spellings as needed
4. Document any new patterns you discover
5. Update these rules for future reference
