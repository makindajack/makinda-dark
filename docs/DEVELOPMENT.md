# Development Guide

This guide covers local development, testing, and debugging of the Makinda Dark theme.

## Quick Start

```bash
# Clone the repository
git clone https://github.com/makindajack/makinda-dark.git
cd makinda-dark

# Open in VS Code
code .

# Press F5 to launch Extension Development Host
```

## Project Structure

```
makinda-dark/
├── .vscode/              # VS Code workspace settings
├── docs/                 # Documentation
│   ├── CONTRIBUTING.md
│   ├── DEVELOPMENT.md
│   ├── INSTALLATION.md
│   └── PUBLISHING.md
├── images/               # Extension assets
│   └── icon.png          # Extension icon (128x128)
├── themes/               # Theme definitions
│   └── Makinda Dark-color-theme.json
├── .gitignore
├── .vscodeignore         # Files excluded from package
├── CHANGELOG.md
├── LICENSE
├── package.json          # Extension manifest
└── README.md
```

## Theme File Anatomy

The theme file (`themes/Makinda Dark-color-theme.json`) contains:

### Header

```json
{
  "name": "Makinda Dark",
  "type": "dark",
  "semanticHighlighting": true,
  ...
}
```

### Semantic Token Colors

Modern VS Code feature for language-aware highlighting:

```json
"semanticTokenColors": {
  "enumMember": { "foreground": "#b88ef2" },
  "variable.constant": { "foreground": "#ff8d37" }
}
```

### Token Colors (TextMate Scopes)

Traditional syntax highlighting:

```json
"tokenColors": [
  {
    "name": "Comments",
    "scope": "comment, punctuation.definition.comment",
    "settings": {
      "fontStyle": "italic",
      "foreground": "#6b7280"
    }
  }
]
```

### UI Colors

Editor and workbench colors:

```json
"colors": {
  "editor.background": "#0e0e0f",
  "editor.foreground": "#e7e8ea",
  "activityBar.background": "#0e0e0f"
  // ... 200+ more
}
```

## Development Workflow

### 1. Launch Development Mode

1. Open the project in VS Code
2. Press `F5` or click `Run → Start Debugging`
3. A new VS Code window opens with your theme active
4. Make changes → Save → Theme updates automatically (usually)

### 2. Manual Reload

If changes don't appear:

1. In the Extension Development Host window
2. Press `Ctrl+Shift+P` → `Developer: Reload Window`

### 3. Inspecting Elements

To find the correct scope for syntax highlighting:

1. Open a source file in Extension Development Host
2. Press `Ctrl+Shift+P` → `Developer: Inspect Editor Tokens and Scopes`
3. Click on any token to see its scopes
4. Use those scopes in your `tokenColors` array

## Color Reference

### Primary Palette

| Name           | Hex       | Usage                   |
| -------------- | --------- | ----------------------- |
| Background     | `#0e0e0f` | Editor, sidebars        |
| Surface 1      | `#1e2022` | Active elements, inputs |
| Surface 2      | `#26282c` | Hover states            |
| Border         | `#36393f` | Dividers, frames        |
| Text Primary   | `#e7e8ea` | Main text               |
| Text Secondary | `#969ba6` | Dimmed text             |
| Text Muted     | `#6b7280` | Comments, placeholders  |

### Accent Colors

| Name       | Hex       | Usage                 |
| ---------- | --------- | --------------------- |
| Orange 500 | `#ff6b0d` | Keywords, accents     |
| Orange 400 | `#ff8d37` | Functions             |
| Orange 300 | `#ffb770` | Constants, attributes |
| Purple 400 | `#a78bfa` | Types, classes        |
| Purple 300 | `#b88ef2` | Support functions     |
| Teal       | `#2dd4bf` | Strings               |
| Cyan       | `#22d3ee` | Links, regex          |

### Semantic Colors

| Name    | Hex       | Usage              |
| ------- | --------- | ------------------ |
| Error   | `#f87171` | Errors, deleted    |
| Warning | `#fbbf24` | Warnings, modified |
| Success | `#4ade80` | Added, success     |
| Info    | `#60a5fa` | Info, hints        |

## Testing Checklist

### Language Support

Test with various file types:

- [ ] JavaScript/TypeScript (`.js`, `.ts`, `.jsx`, `.tsx`)
- [ ] Python (`.py`)
- [ ] HTML/CSS/SCSS (`.html`, `.css`, `.scss`)
- [ ] JSON/YAML (`.json`, `.yaml`)
- [ ] Markdown (`.md`)
- [ ] Rust (`.rs`)
- [ ] Go (`.go`)
- [ ] Java (`.java`)

### UI Elements

Verify these UI components:

- [ ] Activity Bar
- [ ] Side Bar (Explorer, Search, Git, etc.)
- [ ] Editor tabs
- [ ] Editor area
- [ ] Terminal
- [ ] Status Bar
- [ ] Title Bar
- [ ] Breadcrumbs
- [ ] Minimap
- [ ] Notifications
- [ ] Command Palette
- [ ] Quick Open
- [ ] Settings UI
- [ ] Debug views

### Special Features

- [ ] Git decorations (added/modified/deleted)
- [ ] Error/warning squiggles
- [ ] Bracket matching
- [ ] Search highlights
- [ ] Selection highlights
- [ ] Diff editor
- [ ] Merge conflicts
- [ ] Code folding

## Common Tasks

### Adding a New Token Color

1. Use scope inspector to find the scope
2. Add to `tokenColors` array:

```json
{
  "name": "Your Description",
  "scope": "your.scope.here",
  "settings": {
    "foreground": "#ff6b0d"
  }
}
```

### Adding a UI Color

1. Find the color key in [VS Code Theme Reference](https://code.visualstudio.com/api/references/theme-color)
2. Add to `colors` object:

```json
"newElement.color": "#ff6b0d"
```

### Debugging Colors

1. Open Developer Tools: `Help → Toggle Developer Tools`
2. Use Inspect Element on UI components
3. Look for CSS custom properties starting with `--vscode-`

## Tools & Resources

### Useful Commands

```bash
# Package extension
vsce package

# List package contents
vsce ls

# Test install locally
code --install-extension makinda-dark-1.0.0.vsix

# Validate package.json
npx vsce ls --packagedDependencies
```

### References

- [Theme Color Reference](https://code.visualstudio.com/api/references/theme-color)
- [TextMate Scopes](https://macromates.com/manual/en/language_grammars)
- [Semantic Highlighting](https://code.visualstudio.com/api/language-extensions/semantic-highlight-guide)
- [Color Theme Guide](https://code.visualstudio.com/api/extension-guides/color-theme)

### Color Tools

- [Coolors](https://coolors.co/) - Color palette generator
- [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/) - Accessibility
- [VS Code Theme Studio](https://themes.vscode.one/) - Visual theme editor

## Debugging

### Theme Not Loading

1. Check for JSON syntax errors
2. Validate theme path in `package.json`
3. Check VS Code Output panel for errors

### Colors Not Applying

1. Wrong scope - use scope inspector
2. Scope specificity - more specific scopes override general ones
3. Semantic highlighting may override token colors

### Performance Issues

1. Minimize regex in scopes
2. Don't duplicate token rules
3. Keep file size reasonable

## Release Process

1. Update version in `package.json`
2. Update `CHANGELOG.md`
3. Test thoroughly
4. Create git tag:
   ```bash
   git tag v1.0.0
   git push origin v1.0.0
   ```
5. Package: `vsce package`
6. Publish: `vsce publish`

See [PUBLISHING.md](PUBLISHING.md) for detailed publishing instructions.
