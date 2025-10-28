# Setting Up Quick Select Patterns in WezTerm

## Foreword

I started using WezTerm back in 2022. I chose it over Alacritty because it supported tabs out of the box. Even though I don't use WezTerm's tabs anymore (as I use Zellij for multiplexing sessions), there is one feature I can't live without: [quick select patterns](https://wezterm.org/quickselect.html).

This manual will show you how to configure WezTerm's quick select patterns to work seamlessly with Nushell's structured output. You'll learn what quick select patterns are, why they're useful, and how to set them up specifically for Nushell workflows.

## What Are Quick Select Patterns?

Quick select patterns are regular expressions that tell WezTerm what text to recognize and select in your terminal output. When you activate quick select mode (with `Ctrl+Shift+Space` by default), WezTerm highlights all matching patterns, letting you quickly select and copy them without using your mouse.

This is especially powerful with Nushell because:
- Nushell outputs structured tables with consistent patterns
- Error messages include file paths with line numbers
- You frequently need to copy paths, values, or specific cells from table output

Instead of carefully selecting text with your mouse (which is slow and error-prone), you can press a shortcut, type a number or letter hint, and instantly copy exactly what you need.

## Configuring Quick Select Patterns

Let's set up patterns optimized for Nushell workflows.

### Step 1: Open WezTerm Configuration

Open your WezTerm configuration file:

```nu
# Open wezterm.lua in VS Code
code ~/.config/wezterm/wezterm.lua
```

### Step 2: Add Quick Select Patterns

Add this block to your config somewhere **before** the `return config` statement:

```lua
local quick_select_patterns = {
  -- Nushell error paths (like ╭─[/path/to/file.nu:1946:63])
  "─\\[(.*\\:\\d+\\:\\d+)\\]",

  -- Table patterns
  -- $env.config.table.mode = "default"
  -- $env.config.table.header_on_separator = true
  -- $env.config.footer_mode = "always"
  "(?<=─|╭|┬)([a-zA-Z0-9 _%.-]+?)(?=─|╮|┬)", -- Headers
  "(?<=│ )([a-zA-Z0-9 _.-]+?)(?= │)", -- Column values

  -- File paths (stops at ~, allows dots in path but stops before dot+space)
  "/[^/\\s│~]+(?:/[^/\\s│~]+)*(?:\\.(?!\\s)[a-zA-Z0-9]+)?",
}

config.quick_select_patterns = quick_select_patterns
```

> [!NOTE]
> These patterns are designed to work with Nushell's default table formatting. The comments show which Nushell config settings they expect.

Save the file.

### Step 3: Configure Nushell Table Settings

For the quick select patterns above to work as demonstrated, configure Nushell's table output to match the author's setup:

```nu
# Open your Nushell config
config nu
```

Add these settings anywhere in your `config.nu`:

```nu
$env.config.table.header_on_separator = true
$env.config.footer_mode = "always"
```

Save the file and restart Nushell.

## Using Quick Select

Now let's see quick select in action.

### Example 1: Selecting from Nushell Tables

Try this in your terminal:

```nu
# List files with details
ls
```

You'll see a table output. Now press `Ctrl+Shift+Space` to activate quick select mode. WezTerm will highlight:
- Column headers (name, size, modified)
- Individual cell values in each column
- Any file paths

Each highlighted match shows a letter or number hint. Press the corresponding key to copy that value to your clipboard.

### Example 2: Copying Error Paths

Quick select really shines when you encounter Nushell errors:

```nu
# This will produce an error with a file path
source /path/to/nonexistent/file.nu
```

When you see an error like:

```
Error: nu::shell::file_not_found

  × File not found
   ╭─[/path/to/file.nu:1946:63]
```

Press `Ctrl+Shift+Space`, and the path `/path/to/file.nu:1946:63` will be highlighted and ready to copy.

## What's Next?

Congratulations! You've configured WezTerm's quick select feature to work beautifully with Nushell's structured output.

This feature will save you significant time as you work with Nushell, especially when:
- Debugging scripts and copying error paths
- Extracting specific values from table output
- Copying file paths for further processing
- Working with structured data pipelines

As you continue your Nushell journey, you'll find quick select becoming second nature. The next manual will explore more Nushell configuration and workflows to further enhance your productivity. Happy selecting!
