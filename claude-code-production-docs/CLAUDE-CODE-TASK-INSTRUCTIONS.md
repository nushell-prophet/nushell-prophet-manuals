# Claude Code Task Instructions for nushell-prophet-manuals

This document contains instructions for executing typical tasks in the nushell-prophet-manuals project, tailored to the user's preferences and workflow patterns.

## User Preferences

### Communication Style
- **Prompt Rephrasing**: Before executing EVERY prompt, rephrase it for clarity in ENGLISH and print to console (even if the initial request was in Russian)
- **Concise Responses**: User works in terminal - keep responses short and to the point
- **Direct Execution**: User often uses short commands like "edit", "apply", "fix", "correct", or numbered choices (1, 2, 3) - execute these immediately
- **No Emojis**: Never use emojis in communication unless explicitly requested

### Language and Grammar
- **Proactive Grammar Fixing**: User is a non-native English speaker - always proactively check and fix:
  - Articles (a/an/the)
  - Prepositions
  - Verb tenses
  - Awkward phrasing
  - Clarity issues
- **Edit in Place**: When user says "correct" or "fix", edit the selected text directly
- **Style Explanations**: Occasionally provide brief, helpful explanations when making edits (e.g., "Oxford comma for clarity"), but keep them concise

## Common Task Patterns

### 1. Grammar and Clarity Corrections

**Triggers**: "correct", "check", "fix", "edit in place", "is this ok?"

**Process**:
1. Read the selected text or referenced file
2. Identify grammar, clarity, and style issues
3. Fix articles, prepositions, verb tenses
4. Rephrase awkward sentences
5. Apply edits using the Edit tool
6. Briefly explain significant changes if helpful

**Example**:
```
User: <selected-text>...text...</selected-text> correct
→ Read text, fix all issues, apply Edit tool, confirm changes
```

### 2. Creating Pull Requests

**Triggers**: "create pr", "make a pr", "prepare a pr to main"

**Process**:
1. Run `git status` to see changes
2. Run `git diff` to see specific modifications
3. Run `git log` to see recent commit style
4. Analyze changes and draft PR description
5. Push to remote with `git push -u origin [branch]` if needed
6. Create PR using `gh pr create` with detailed description

**PR Description Format**:
```markdown
## Summary
- [Bullet point summary of changes]

## Test plan
- [Checklist of what was tested/verified]

🤖 Generated with [Claude Code](https://claude.com/claude-code)
```

### 3. Writing YouTube Descriptions

**Triggers**: "write youtube description to @manuals/NN-.../manual.md"

**Process**:
1. Read the corresponding manual.md file thoroughly
2. Read YOUTUBE-DESCRIPTION-GUIDELINES.md for complete structure and requirements
3. Create youtube-description.md in the manual's folder following all guidelines

**Key Requirements**:
- Follow structure from YOUTUBE-DESCRIPTION-GUIDELINES.md exactly
- NO external links - all resources should be in the manual

### 4. Alignment Checks

**Triggers**: "check @README.md versus @manual", "align it with other manuals", "check alignment"

**Process**:
1. Read both files being compared
2. Check for consistency in:
   - Section headings and structure
   - Writing style and tone
   - Technical accuracy
   - Grammar and clarity
   - Formatting conventions
3. Report discrepancies
4. If user says "fix" or "edit", apply corrections using Edit tool
5. Ensure README.md bullet points mirror manual.md major sections

### 5. Applying TTS Preparation Rules

**Triggers**: "apply @TTS-PREPARATION-RULES.md", "prepare for tts"

**Process**:
1. Read TTS-PREPARATION-RULES.md for complete transformation rules
2. Read the target file (usually video-narration.md)
3. Apply all transformations per the rules document
4. Edit the file in place
5. Confirm changes applied

### 6. Adding Metadata/Frontmatter

**Triggers**: "add meta:", "frontmatter to manual:", "add the yaml"

**Process**:
1. Read the manual.md file
2. Extract YouTube and Telegram links from user's message
3. Add YAML frontmatter at the top of manual.md:
```yaml
---
youtube: https://youtu.be/[VIDEO_ID]
telegram: https://t.me/nushellprophet/[POST_NUMBER]
---
```
4. Apply using Edit tool
5. If old meta.yaml files exist, remove them

### 7. Updating README.md

**Triggers**: "update @README.md", "add info about manual NN to readme"

**Process**:
1. Read the new or updated manual.md file
2. Read current README.md
3. Extract main sections from the manual
4. Add or update the manual entry in README.md with:
   - Manual number and title
   - Brief description (1-2 sentences)
   - Bulleted list of main sections
   - Link to manual: `manuals/NN-descriptive-name/manual.md`
5. Maintain consistent formatting with existing entries
6. Apply edits using Edit tool

### 8. Creating or Editing Video Narration

**Triggers**: "create video narration", "edit @video-narration.md", "rewrite for tts"

**Process**:
1. Read the source manual.md file
2. Read TTS-PREPARATION-RULES.md for all phonetic and formatting rules
3. Convert manual content to narration style:
   - First-person narrative ("I'll", "Let's")
   - Conversational tone
   - Apply all TTS rules from the dedicated rules document
   - Add natural transitions
   - Include "commands from manual" references
4. Create or update video-narration.md
5. Ensure it flows naturally when read aloud

### 9. Committing Changes

**Triggers**: User runs `/commit-git` slash command (automatic), or says "commit"

**Process**:
1. Run in parallel:
   - `git status` to see all untracked files
   - `git diff` to see staged and unstaged changes
   - `git log -n 5 --oneline` to see recent commit message style
2. Analyze changes and draft commit message:
   - Summarize nature of changes (new feature, enhancement, bug fix, docs, etc.)
   - Focus on "why" rather than "what"
   - Keep it concise (1-2 sentences)
3. Add relevant untracked files with `git add`
4. Create commit with heredoc format:
```bash
git commit -m "$(cat <<'EOF'
[Commit message]

🤖 Generated with [Claude Code](https://claude.com/claude-code)

Co-Authored-By: Claude <noreply@anthropic.com>
EOF
)"
```
5. Run `git status` after commit to verify success

### 10. Research and Exploration

**Triggers**: "research all markdown files", "find where X is used", "what is the codebase structure"

**Process**:
1. Use Task tool with subagent_type=Explore for open-ended searches
2. For specific files: use Glob tool with pattern like `**/*.md`
3. For specific content: use Grep tool with appropriate pattern
4. Provide comprehensive summary of findings
5. Never use bash find/grep commands - always use specialized tools

## File Organization Patterns

### Manual Structure (Required)
```
manuals/NN-descriptive-name/
├── manual.md                    # Main content (REQUIRED)
├── youtube-description.md       # YouTube description (REQUIRED for videos)
├── video-narration.md          # TTS script (optional)
└── media/                      # Screenshots (optional)
    └── *.png
```

### Frontmatter in manual.md
```yaml
---
youtube: https://youtu.be/VIDEO_ID
telegram: https://t.me/nushellprophet/POST_NUMBER
---
```

### File Naming Conventions
- Manuals: Zero-padded numbers (01-, 02-, 03-)
- Descriptive kebab-case names
- Pattern: `NN-descriptive-name`

## Content Guidelines

### Writing Style
- **Target Audience**: Beginners ("nu-bies")
- **Tone**: Encouraging, practical, step-by-step
- **Voice**: First-person when appropriate
- **Clarity**: Explain "why" behind actions, not just "what"
- **Code Examples**: Always include comments explaining purpose

### Manual Sections (Typical)
1. Title (H1)
2. Foreword (context, prerequisites, optional status)
3. Main instructional sections (H2 headings)
4. What's Next? (closing, encouragement, forward reference)

### Code Blocks
- Always tag with language: ````nu`, ````bash`, ````lua`
- Include explanatory comments
- Show verification steps after major changes

### Notes and Callouts
Use markdown blockquote syntax:
```markdown
> [!NOTE]
> Important information here
```

## Quality Checklist

Before considering any manual complete, verify:

- [ ] Grammar and clarity reviewed throughout
- [ ] All code blocks properly tagged
- [ ] Commands include explanatory comments
- [ ] Screenshots in `media/` folder (if applicable)
- [ ] Frontmatter with YouTube/Telegram links added
- [ ] YouTube description created following guidelines
- [ ] README.md updated with manual entry
- [ ] Consistent style with other manuals
- [ ] "What's Next?" section included
- [ ] Git committed with proper message format

## Special Workflows

### Publishing a New Manual (Complete Process)

When user is ready to publish a new manual:

1. **Content Review**
   - Read entire manual.md
   - Check grammar and clarity throughout
   - Verify all code examples work
   - Ensure consistent style with other manuals

2. **Supporting Files**
   - Create youtube-description.md following guidelines
   - Create video-narration.md if needed (apply TTS rules)
   - Ensure all screenshots in media/ folder

3. **Metadata**
   - Add frontmatter to manual.md (YouTube and Telegram links)
   - Remove any old meta.yaml files

4. **README Update**
   - Add manual entry to README.md
   - Include bulleted section list
   - Verify link path is correct

5. **Git Workflow**
   - Stage all changes
   - Commit with descriptive message
   - Create PR to main branch
   - Include comprehensive PR description

### Translating and Syncing Narration

When working with Russian narration:

1. Read both narration_ru.txt and narration.txt (if exists)
2. Correct errors in Russian version first
3. Translate Russian to English
4. Apply TTS-PREPARATION-RULES.md to English version
5. Ensure both versions have same semantic content
6. Save as narration.txt with TTS-ready formatting

## Quick Reference Commands

**User says** → **Claude does**

- "correct" → Read, fix grammar/clarity, apply Edit tool
- "fix" → Same as correct
- "edit in place" → Apply edits directly to file
- "1" or "2" → Choose the numbered option and apply
- "apply" → Use the suggested change/fix
- "create pr" → Stage, commit, push, create GitHub PR
- "update readme" → Add/update manual entry in README.md
- "check alignment" → Compare files for consistency
- "/commit-git" → Automated git commit workflow
- "research" → Use Task/Explore for comprehensive search

## Advanced Patterns

### When User Provides Selected Text
```
<selected-text file="path" lines="N-M">...</selected-text>
```
- This is the exact text to work with
- Apply changes to this specific section
- Use Edit tool with exact old_string match
- Preserve indentation and formatting

### When User Says "ok?"
- User wants validation/confirmation
- Provide brief assessment
- Point out any issues or improvements
- Ask for confirmation if multiple approaches exist

### When User Provides Russian Text
- Rephrase the request in English first (per global CLAUDE.md rule)
- Then proceed with the task
- Be mindful of translation nuances

### When User References Another Manual
Format: `@manuals/NN-name/manual.md`
- Always read the referenced manual
- Use it as a style/structure reference
- Maintain consistency in approach

## Project Context

For project overview, channel mission, and content structure, see the main `CLAUDE.md` file in the repository root.

## Technical Notes

- User works in macOS environment
- Uses git (not jj) in this repository
- Prefers VS Code as editor reference for beginners
- Uses Helix personally (mention in forewords)
- All videos recorded on virtual machines to capture fresh setup
- XDG_CONFIG_HOME standard is important for avoiding spaces in paths
- Git version control for configs is emphasized in tutorials
