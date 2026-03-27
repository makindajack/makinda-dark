# Contributing to Makinda Dark

Thank you for your interest in contributing to Makinda Dark! This document provides guidelines and instructions for contributing.

## Code of Conduct

Please be respectful and considerate in all interactions. We welcome contributors of all backgrounds and experience levels.

## How to Contribute

### Reporting Bugs

1. **Check Existing Issues** - Search [GitHub Issues](https://github.com/makindajack/makinda-dark/issues) to avoid duplicates
2. **Create a New Issue** - Use the bug report template
3. **Provide Details**:
   - VS Code version
   - Extension version
   - Operating system
   - Steps to reproduce
   - Screenshots if applicable

### Suggesting Enhancements

1. Open a [GitHub Issue](https://github.com/makindajack/makinda-dark/issues)
2. Use the feature request template
3. Describe the enhancement and its benefits

### Submitting Changes

#### Prerequisites

- [Node.js](https://nodejs.org/) (v18 or higher)
- [Git](https://git-scm.com/)
- [Visual Studio Code](https://code.visualstudio.com/)

#### Setup

```bash
# Fork the repository on GitHub

# Clone your fork
git clone https://github.com/YOUR_USERNAME/makinda-dark.git
cd makinda-dark

# Add upstream remote
git remote add upstream https://github.com/makindajack/makinda-dark.git
```

#### Making Changes

1. **Create a Branch**

   ```bash
   git checkout -b feature/your-feature-name
   # or
   git checkout -b fix/your-bug-fix
   ```

2. **Make Your Changes**
   - Edit theme files in `/themes/`
   - Follow the existing code style
   - Test your changes

3. **Test Locally**
   - Press `F5` in VS Code to launch Extension Development Host
   - Verify your changes look correct

4. **Commit Changes**

   ```bash
   git add .
   git commit -m "feat: description of your changes"
   ```

   Follow [Conventional Commits](https://www.conventionalcommits.org/):
   - `feat:` - New feature
   - `fix:` - Bug fix
   - `docs:` - Documentation changes
   - `style:` - Color/style changes
   - `refactor:` - Code refactoring

5. **Push and Create PR**
   ```bash
   git push origin feature/your-feature-name
   ```

   - Open a Pull Request on GitHub
   - Fill out the PR template
   - Link related issues

## Development Guidelines

### Theme File Structure

```
themes/
└── Makinda Dark-color-theme.json
    ├── name           # Theme name
    ├── type           # "dark" or "light"
    ├── semanticTokenColors  # Semantic highlighting
    ├── tokenColors    # Syntax highlighting rules
    └── colors         # UI colors
```

### Color Guidelines

**Primary Colors:**
| Purpose | Color | Hex |
|---------|-------|-----|
| Background | Near Black | `#0e0e0f` |
| Foreground | Light Gray | `#e7e8ea` |
| Accent | Orange | `#ff6b0d` |
| Secondary | Purple | `#a78bfa` |
| Strings | Teal | `#2dd4bf` |

**Rules:**

- Maintain WCAG AA contrast ratios
- Test colors in different lighting conditions
- Keep the orange/purple/teal color identity
- Use transparency sparingly

### Adding Token Colors

```json
{
  "name": "Description of what this styles",
  "scope": "scope.name.here",
  "settings": {
    "foreground": "#color",
    "fontStyle": "italic" // optional
  }
}
```

### Adding UI Colors

```json
{
  "colors": {
    "element.property": "#color"
  }
}
```

Reference: [VS Code Theme Color Reference](https://code.visualstudio.com/api/references/theme-color)

## Testing Checklist

Before submitting, verify:

- [ ] Theme loads without errors
- [ ] Colors render correctly in Extension Development Host
- [ ] JavaScript/TypeScript syntax looks good
- [ ] Python syntax looks good
- [ ] HTML/CSS syntax looks good
- [ ] Markdown renders properly
- [ ] Terminal colors are readable
- [ ] Git diff colors are visible
- [ ] Error/warning colors are distinguishable
- [ ] UI elements (sidebar, tabs, etc.) look correct

## Pull Request Process

1. Update CHANGELOG.md with your changes
2. Ensure all tests pass
3. Request review from maintainers
4. Address feedback promptly
5. Once approved, changes will be merged

## Style Guide

### JSON Formatting

- Use 2-space indentation
- Keep properties sorted alphabetically where possible
- Use lowercase hex colors

### Naming Conventions

- Use descriptive names for token scopes
- Follow existing naming patterns

## Recognition

Contributors will be:

- Listed in release notes
- Thanked in our README (for significant contributions)

## Questions?

- Open a [Discussion](https://github.com/makindajack/makinda-dark/discussions)
- Email: jacksonmakinda@outlook.com

Thank you for contributing! 🎉
