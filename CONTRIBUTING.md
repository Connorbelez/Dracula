# Contributing to Dracula Enhanced

Thanks for your interest in contributing to Dracula Enhanced! This guide will help you get started.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Setup](#development-setup)
- [Making Changes](#making-changes)
- [Testing Your Changes](#testing-your-changes)
- [Submitting Changes](#submitting-changes)
- [Color Guidelines](#color-guidelines)
- [Common Tasks](#common-tasks)

## Code of Conduct

This project follows a simple code of conduct:
- Be respectful and considerate
- Welcome newcomers and help them learn
- Focus on constructive feedback
- Keep discussions on-topic

## Getting Started

### Prerequisites

- Node.js 16+ and npm
- Visual Studio Code
- Git
- A GitHub account

### Fork and Clone

1. Fork the repository on GitHub
2. Clone your fork:
   ```bash
   git clone https://github.com/YOUR_USERNAME/dracula-enhanced.git
   cd dracula-enhanced
   ```
3. Add the upstream remote:
   ```bash
   git remote add upstream https://github.com/connor/dracula-enhanced.git
   ```

## Development Setup

1. Install dependencies:
   ```bash
   npm install
   ```

2. Build the theme:
   ```bash
   npm run build
   ```

3. The theme files will be generated in the `theme/` directory

## Making Changes

### Understanding the Structure

```
Dracula/
├── src/
│   └── dracula.yml          # Main theme source (EDIT THIS)
├── theme/                    # Generated theme files (DON'T EDIT)
│   ├── dracula.json
│   └── dracula-soft.json
├── scripts/
│   ├── build.js             # Build script
│   ├── generate.js          # Theme generator
│   └── lint.js              # Linter
├── package.json             # Extension manifest
└── README.md
```

### Edit the Source

**IMPORTANT**: Only edit `src/dracula.yml` - never edit the JSON files in `theme/` directly!

The YAML file structure:
```yaml
dracula:
  base:                       # Base color definitions
    - &ORANGE '#FFB86C'
    - &PURPLE '#BD93F9'
    # ... etc

colors:                       # UI colors (sidebar, tabs, etc)
  editor.background: *BG
  # ... etc

tokenColors:                  # Syntax highlighting
  - name: Function parameters
    scope:
      - variable.parameter
    settings:
      foreground: *ORANGE
```

### Color References

Use YAML anchors for colors:
```yaml
# Define
- &ORANGE '#FFB86C'

# Use
foreground: *ORANGE
```

Available colors:
- `*BG` - Background
- `*FG` - Foreground
- `*SELECTION` - Selection
- `*COMMENT` - Comments
- `*CYAN` - Cyan
- `*GREEN` - Green
- `*ORANGE` - Orange
- `*PINK` - Pink
- `*PURPLE` - Purple
- `*RED` - Red
- `*YELLOW` - Yellow

## Testing Your Changes

### 1. Build the Theme

```bash
npm run build
```

### 2. Package the Extension

```bash
npm run package
```

This creates a `.vsix` file in the `bin/` directory.

### 3. Install in VSCode

**Option A: Command Line**
```bash
code --install-extension bin/dracula-enhanced-*.vsix
```

**Option B: VSCode UI**
1. Open VSCode
2. Press `Cmd/Ctrl + Shift + P`
3. Type "Install from VSIX"
4. Select your `.vsix` file

### 4. Test Your Changes

1. Switch to the theme: `Cmd/Ctrl + K` then `Cmd/Ctrl + T`
2. Select "Dracula Enhanced"
3. Open files in different languages:
   - TypeScript/JavaScript
   - Python
   - Go
   - CSS/SCSS
   - JSON
   - Markdown

### 5. Use Token Inspector

To see what scopes are being applied:
1. Press `Cmd/Ctrl + Shift + P`
2. Type "Developer: Inspect Editor Tokens and Scopes"
3. Click on any token to see its scopes
4. Use this info to target the right scopes in `dracula.yml`

## Submitting Changes

### Before Submitting

- [ ] Test the theme with multiple languages
- [ ] Run `npm run lint` (if applicable)
- [ ] Build without errors: `npm run build`
- [ ] Package successfully: `npm run package`
- [ ] Install and test the `.vsix` file
- [ ] Document changes in CHANGELOG.md

### Creating a Pull Request

1. Create a new branch:
   ```bash
   git checkout -b feature/improve-python-highlighting
   ```

2. Make your changes and commit:
   ```bash
   git add src/dracula.yml
   git commit -m "feat: improve Python docstring colors"
   ```

3. Push to your fork:
   ```bash
   git push origin feature/improve-python-highlighting
   ```

4. Open a Pull Request on GitHub

### Commit Message Format

Use conventional commits:

- `feat:` - New feature
- `fix:` - Bug fix
- `docs:` - Documentation changes
- `style:` - Formatting changes (not code style)
- `refactor:` - Code refactoring
- `test:` - Adding tests
- `chore:` - Maintenance tasks

Examples:
```
feat: add better support for Rust highlighting
fix: correct parameter color in function bodies
docs: update installation instructions
style: adjust property colors for better contrast
```

## Color Guidelines

### Dracula Color Palette

Stick to the official Dracula colors:

| Color  | Hex       | Usage                           |
|--------|-----------|----------------------------------|
| Pink   | `#FF79C6` | Keywords, HTML tags             |
| Purple | `#BD93F9` | **Properties**, Constants       |
| Cyan   | `#8BE9FD` | Classes, Built-in types         |
| Green  | `#50FA7B` | Functions, Strings              |
| Orange | `#FFB86C` | **Parameters**, Numbers         |
| Yellow | `#F1FA8C` | Strings, Attributes             |
| Red    | `#FF5555` | Errors, Deletions               |

### Enhanced Features

Our specific enhancements:
- **Parameters**: Orange (`#FFB86C`) everywhere
- **Properties**: Purple (`#BD93F9`) for distinction
- **Variables**: Default foreground (`#F8F8F2`)

### When Adding New Scopes

1. Check if a scope already exists for similar purposes
2. Use the Token Inspector to find the exact scope name
3. Group related scopes together
4. Add comments explaining non-obvious choices
5. Test across multiple languages

Example:
```yaml
- name: Object properties
  scope:
    - support.variable.property          # JavaScript/TypeScript
    - variable.other.property            # General property access
    - variable.other.object.property     # Object property access
    - meta.object-literal.key            # Object literal keys
  settings:
    foreground: *PURPLE
```

## Common Tasks

### Adding Support for a New Language

1. Install the language extension in VSCode
2. Create a test file with various syntax elements
3. Use Token Inspector to identify scopes
4. Add appropriate scope mappings in `dracula.yml`
5. Test thoroughly
6. Document in PR description

### Adjusting a Color

1. Find the scope in `src/dracula.yml`
2. Change the color reference (e.g., `*ORANGE` to `*PURPLE`)
3. Rebuild: `npm run build`
4. Reinstall and test
5. Take before/after screenshots for PR

### Fixing a Bug

1. Reproduce the issue
2. Use Token Inspector to identify the problematic scope
3. Search for that scope in `src/dracula.yml`
4. Fix or add the appropriate mapping
5. Test the fix
6. Add a note to CHANGELOG.md

### Testing Against Official Dracula

To compare with the official theme:

1. Install official Dracula: `ext install dracula-theme.theme-dracula`
2. Open a file side-by-side
3. Switch between themes: `Cmd/Ctrl + K` then `Cmd/Ctrl + T`
4. Note differences
5. Verify enhancements align with project goals

## Resources

### VSCode Theme Documentation

- [Theme Color Reference](https://code.visualstudio.com/api/references/theme-color)
- [Syntax Highlight Guide](https://code.visualstudio.com/api/language-extensions/syntax-highlight-guide)
- [TextMate Scopes](https://macromates.com/manual/en/language_grammars)

### Dracula Specification

- [Dracula Spec](https://spec.draculatheme.com/)
- [Dracula UI Specification](https://spec.draculatheme.com/ui)

### Tools

- [Token Inspector](https://code.visualstudio.com/api/language-extensions/syntax-highlight-guide#scope-inspector)
- [TmTheme Editor](https://tmtheme-editor.herokuapp.com/) - Preview theme online
- [VSCode Theme Studio](https://themes.vscode.one/) - Theme builder

## Getting Help

- **Questions**: Open a GitHub Discussion
- **Bugs**: Open a GitHub Issue with:
  - VSCode version
  - Steps to reproduce
  - Expected vs actual behavior
  - Screenshots (if applicable)
- **Feature Requests**: Open a GitHub Issue describing:
  - The feature
  - Use case
  - Example (if applicable)

## Recognition

Contributors will be:
- Listed in the project README
- Mentioned in release notes
- Credited in CHANGELOG.md

Thank you for contributing to Dracula Enhanced! 🦇🎨