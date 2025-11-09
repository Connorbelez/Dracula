# Dracula Enhanced

A dark theme for [Visual Studio Code](https://code.visualstudio.com) based on the popular [Dracula](https://draculatheme.com/) color scheme, with enhanced semantic highlighting for better code readability.

![Dracula Enhanced](./screenshot.png)

## What's Enhanced?

This theme improves upon the original Dracula theme with better color differentiation for:

- **Function Parameters** - Orange (#FFB86C) everywhere, both in declarations and usage
- **Object Properties** - Lavender purple (#BD93F9) for clear distinction from variables
- **Variables** - Default foreground color for clean contrast

### The Problem This Solves

In the original Dracula theme, function parameters and object properties often had the same color as regular variables, making it harder to scan code quickly. This enhanced version uses semantic highlighting to provide better visual separation.

## Installation

### From VSCode Marketplace

1. Open **Extensions** sidebar panel in VS Code. `View → Extensions`
2. Search for `Dracula Enhanced`
3. Click **Install**
4. Click **Reload** to reload your editor
5. Code → Preferences → Color Theme → **Dracula Enhanced**

### Manual Installation

1. Clone this repository
2. Run `npm install`
3. Run `npm run build`
4. Run `npm run package`
5. Install the generated `.vsix` file in VS Code

## Color Palette

| Palette      | Hex       | RGB           | HSL             | Usage                    |
| ------------ | --------- | ------------- | --------------- | ------------------------ |
| Background   | `#282a36` | `40 42 54`    | `231° 15% 18%`  | Background               |
| Current Line | `#44475a` | `68 71 90`    | `232° 14% 31%`  | Current Line, Selection  |
| Foreground   | `#f8f8f2` | `248 248 242` | `60° 30% 96%`   | Regular variables        |
| Comment      | `#6272a4` | `98 114 164`  | `225° 27% 51%`  | Comments                 |
| Cyan         | `#8be9fd` | `139 233 253` | `191° 97% 77%`  | Classes, Built-ins       |
| Green        | `#50fa7b` | `80 250 123`  | `135° 94% 65%`  | Functions, Strings       |
| Orange       | `#ffb86c` | `255 184 108` | `31° 100% 71%`  | **Parameters** (Enhanced)|
| Pink         | `#ff79c6` | `255 121 198` | `326° 100% 74%` | Keywords                 |
| Purple       | `#bd93f9` | `189 147 249` | `265° 89% 78%`  | **Properties** (Enhanced)|
| Red          | `#ff5555` | `255 85 85`   | `0° 100% 67%`   | Errors                   |
| Yellow       | `#f1fa8c` | `241 250 140` | `65° 92% 76%`   | Strings                  |

## Examples

### Before (Original Dracula)
```typescript
function updateUser(ctx: Context, args: { name: string }) {
  const user = ctx.db.get(args.name);  // ctx, args, user all same color
  return user.profile;                  // profile same as user
}
```

### After (Dracula Enhanced)
```typescript
function updateUser(ctx: Context, args: { name: string }) {
  const user = ctx.db.get(args.name);  // ctx, args are ORANGE
  return user.profile;                  // profile is PURPLE, user is default
}
```

## Team

This theme is maintained by:
- Connor

## Credits

Based on the original [Dracula theme](https://draculatheme.com/) by Zeno Rocha and contributors.

## License

[MIT License](./LICENSE)