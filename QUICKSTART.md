# Quick Start Guide - Dracula Enhanced

Get up and running with Dracula Enhanced in 5 minutes!

## 🚀 Quick Install (Local Development)

```bash
# 1. Clone the repository
git clone https://github.com/connor/dracula-enhanced.git
cd dracula-enhanced

# 2. Install dependencies
npm install

# 3. Build the theme
npm run build

# 4. Package the extension
npm run package

# 5. Install in VSCode
code --install-extension bin/dracula-enhanced-*.vsix
```

## 🎨 Activate the Theme

1. Open VSCode
2. Press `Cmd/Ctrl + K` then `Cmd/Ctrl + T`
3. Select **"Dracula Enhanced"**
4. Enjoy! 🦇

## 👀 See the Difference

Open a TypeScript/JavaScript file and notice:

### Before (Original Dracula)
```typescript
function updateUser(ctx: Context, args: { name: string }) {
  const user = ctx.db.get(args.name);  // All same color 😕
  return user.profile;
}
```

### After (Dracula Enhanced)
```typescript
function updateUser(ctx: Context, args: { name: string }) {
  const user = ctx.db.get(args.name);  // ctx, args = ORANGE 🟠
  return user.profile;                  // profile = PURPLE 🟣
}
```

## 🔧 Making Your Own Changes

### Step 1: Edit the Source
```bash
# Open the theme source file
code src/dracula.yml
```

### Step 2: Find What You Want to Change

Use VSCode's Token Inspector:
1. Press `Cmd/Ctrl + Shift + P`
2. Type: "Developer: Inspect Editor Tokens and Scopes"
3. Click on any code to see its scope

### Step 3: Edit Colors

In `src/dracula.yml`:
```yaml
- name: Function parameters
  scope:
    - variable.parameter
    - variable.language.special
  settings:
    foreground: *ORANGE  # Change this to *PURPLE, *GREEN, etc.
    fontStyle: italic
```

### Step 4: Rebuild and Test
```bash
# Rebuild
npm run build

# Package
npm run package

# Reinstall (overwrites previous)
code --install-extension bin/dracula-enhanced-*.vsix --force

# Reload VSCode
# Press Cmd/Ctrl + Shift + P → "Reload Window"
```

## 📋 Available Colors

Use these color references in `src/dracula.yml`:

| Reference | Hex       | Color   | Usage                    |
|-----------|-----------|---------|--------------------------|
| `*PINK`   | `#FF79C6` | 🌸 Pink | Keywords                 |
| `*PURPLE` | `#BD93F9` | 🟣 Purple | **Properties**, Constants |
| `*CYAN`   | `#8BE9FD` | 🔵 Cyan | Classes, Types           |
| `*GREEN`  | `#50FA7B` | 🟢 Green | Functions, Strings       |
| `*ORANGE` | `#FFB86C` | 🟠 Orange | **Parameters**, Numbers   |
| `*YELLOW` | `#F1FA8C` | 🟡 Yellow | Strings, Attributes      |
| `*RED`    | `#FF5555` | 🔴 Red  | Errors                   |
| `*FG`     | `#F8F8F2` | ⚪ White | Variables, Text          |
| `*COMMENT`| `#6272A4` | 💬 Gray | Comments                 |

## 🐛 Troubleshooting

### Theme not showing up?
```bash
# Check build output
npm run build
# Should see: theme/dracula.json created

# Check package
npm run package
# Should see: bin/dracula-enhanced-*.vsix created

# Reinstall with force flag
code --install-extension bin/dracula-enhanced-*.vsix --force
```

### Colors not changing?
1. Make sure you edited `src/dracula.yml` (not the JSON files!)
2. Rebuild: `npm run build`
3. Reload VSCode: `Cmd/Ctrl + Shift + P` → "Reload Window"

### Want to go back to defaults?
```bash
git checkout src/dracula.yml
npm run build
npm run package
code --install-extension bin/dracula-enhanced-*.vsix --force
```

## 📚 Next Steps

- Read [CONTRIBUTING.md](./CONTRIBUTING.md) for detailed development guide
- Read [DEPLOYMENT.md](./DEPLOYMENT.md) for publishing instructions
- Check [CHANGELOG.md](./CHANGELOG.md) for version history

## 🎯 Common Customizations

### Make Comments More Visible
```yaml
- name: Comments
  scope:
    - comment
  settings:
    foreground: *CYAN  # Changed from *COMMENT
```

### Remove Italic from Parameters
```yaml
- name: Function parameters
  scope:
    - variable.parameter
  settings:
    foreground: *ORANGE
    fontStyle: normal  # Changed from italic
```

### Change Property Color
```yaml
- name: Object properties
  scope:
    - support.type.property-name
    - variable.other.property
  settings:
    foreground: *CYAN  # Changed from *PURPLE
```

## 💡 Pro Tips

1. **Keep Token Inspector Open**: It's your best friend for finding scopes
2. **Test Multiple Languages**: Changes might affect more than you think
3. **Use Git**: Commit working changes so you can experiment safely
4. **Compare Themes**: Switch between original Dracula and Enhanced to see differences
5. **Take Screenshots**: Document your changes for pull requests

## 🤝 Share Your Customizations

Found a cool color combo? Share it!

1. Create an issue on GitHub with screenshots
2. Submit a pull request
3. Help others discover better color schemes

## 📞 Need Help?

- **GitHub Issues**: For bugs and feature requests
- **GitHub Discussions**: For questions and ideas
- **Token Inspector**: `Cmd/Ctrl + Shift + P` → "Inspect Editor Tokens"

---

Happy theming! 🦇✨