# Claude Code Plugin Tutorials

Starter templates and tutorials for building Claude Code plugins. No coding required.

**Watch the full tutorial:** [YouTube Video Link]

## What's Inside

### Marketing Plugin
A complete Claude Code plugin for marketers, PMs, and creators. Includes:

| Component | What It Does |
|-----------|-------------|
| `/brand-voice` | Write any content in your brand voice |
| `/social-post` | Generate platform-specific social posts |
| `copywriter` agent | Auto-activates for any persuasive writing |
| Brand voice hook | Automatically checks content matches your style |
| Playwright MCP | Claude can browse websites for competitor research |

## Quick Install

```bash
/plugin add github:talknerdytome-labs/claude-plugin-tutorials/marketing-plugin
```

That's it. You now have access to all the commands, agents, hooks, and MCP tools.

## Manual Setup (Follow Along with Video)

If you want to build it yourself step-by-step:

### Step 1: Create the Plugin Folder

In Cursor's file explorer:
1. Right-click → New Folder → `my-plugin`
2. Inside `my-plugin`, create folder: `.claude-plugin` (don't forget the dot!)
3. Inside `.claude-plugin`, create file: `plugin.json`

```json
{
  "name": "my-plugin",
  "description": "My personal Claude assistant",
  "version": "1.0.0"
}
```

### Step 2: Add Your First Command

1. In `my-plugin`, create folder: `commands`
2. Inside `commands`, create file: `brand-voice.md`

```markdown
---
name: brand-voice
description: Write content in our brand voice
---

When writing content, follow these guidelines:

TONE:
- Conversational but professional
- Confident, not arrogant

WORDS WE USE:
- "You" not "users"
- "Simple" not "easy"

WORDS WE AVOID:
- "Synergy"
- "Leverage"

Now write the content the user requested.
```

### Step 3: Add a Command with Arguments

Create `commands/social-post.md`:

```markdown
---
name: social-post
description: Create a social media post
args:
  - name: platform
    description: twitter, linkedin, or instagram
    required: true
  - name: topic
    description: What to write about
    required: true
---

Create a {{ platform }} post about {{ topic }}.
Follow our brand voice guidelines.
```

Now you can use: `/social-post twitter "product launch"`

### Step 4: Add an Agent

1. In `my-plugin`, create folder: `agents`
2. Inside `agents`, create file: `copywriter.md`

```markdown
---
name: copywriter
description: Use when the user needs marketing copy, ad copy, or persuasive writing
color: purple
---

You are a senior copywriter. When writing copy:

1. Start with the reader's problem
2. Use the PAS framework (Problem, Agitate, Solution)
3. Write at an 8th grade reading level
4. End with a clear call to action
```

The agent activates automatically when Claude detects you need copywriting help.

### Step 5: Add a Hook

Inside `.claude-plugin`, create file: `hooks.json`

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write",
        "hooks": [
          {
            "type": "prompt",
            "prompt": "Does this match our brand voice? Flag anything off-brand."
          }
        ]
      }
    ]
  }
}
```

### Step 6: Add Playwright MCP (Browser Control)

Inside `.claude-plugin`, create file: `.mcp.json`

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["-y", "@playwright/mcp@latest"]
    }
  }
}
```

Restart Claude Code. Now you can ask Claude to browse websites:

> "Go to [competitor.com] and analyze their homepage messaging"

### Step 7: Install Your Plugin

```bash
/plugin add file:///path/to/my-plugin
```

Pro tip: Drag your folder into the terminal to get the exact path.

## Final Structure

```
my-plugin/
├── .claude-plugin/
│   ├── plugin.json
│   ├── hooks.json
│   └── .mcp.json
├── commands/
│   ├── brand-voice.md
│   └── social-post.md
└── agents/
    └── copywriter.md
```

## Customize It

The templates are starting points. Make them yours:

- **Brand voice**: Replace with YOUR tone, YOUR words, YOUR style
- **Social post**: Add your platform-specific guidelines
- **Copywriter**: Add your frameworks and techniques
- **Hooks**: Add checks for your specific requirements

## Resources

- [Official Claude Code Plugins Docs](https://www.anthropic.com/news/claude-code-plugins)
- [Claude Code Plugins Hub (243 plugins)](https://github.com/jeremylongshore/claude-code-plugins-plus)
- [Playwright MCP](https://github.com/microsoft/playwright-mcp)

## Questions?

Drop a comment on the YouTube video or open an issue here. Happy to help!

---

Made with love by [Talk Nerdy to Me](https://youtube.com/@talknerdytome)
