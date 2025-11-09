# Visual Examples - Dracula Enhanced

This document shows examples of the enhanced color scheme in action.

## 🎨 Color Reference

### Enhanced Colors (What Makes This Theme Special)

| Element | Color | Hex | Why |
|---------|-------|-----|-----|
| **Parameters** | 🟠 Orange | `#FFB86C` | Consistent everywhere - declaration AND usage |
| **Properties** | 🟣 Purple | `#BD93F9` | Distinct from variables, easy to spot |
| **Variables** | ⚪ White | `#F8F8F2` | Clean, neutral, readable |

### Standard Dracula Colors (Unchanged)

| Element | Color | Hex |
|---------|-------|-----|
| Keywords | 🌸 Pink | `#FF79C6` |
| Functions | 🟢 Green | `#50FA7B` |
| Strings | 🟡 Yellow | `#F1FA8C` |
| Classes | 🔵 Cyan | `#8BE9FD` |
| Numbers | 🟠 Orange | `#FFB86C` |
| Comments | 💬 Gray | `#6272A4` |

## 📝 TypeScript/JavaScript Examples

### Function Parameters

```typescript
// ✨ ENHANCED: Parameters are orange in declaration AND usage

function updateUser(ctx: Context, args: { name: string }) {
  //               ^^^          ^^^^
  //               🟠 ORANGE    🟠 ORANGE
  
  const user = ctx.db.get(args.name);
  //           ^^^        ^^^^
  //           🟠 ORANGE  🟠 ORANGE
  
  return user.profile;
  //          ^^^^^^^
  //          🟣 PURPLE (property!)
}
```

### Object Properties

```typescript
// ✨ ENHANCED: Properties are purple, variables are white

interface User {
  name: string;      // 🟣 PURPLE
  email: string;     // 🟣 PURPLE
  profile: Profile;  // 🟣 PURPLE
}

const user = {
  name: "Connor",    // 🟣 PURPLE (property name)
  email: "x@y.com"   // 🟣 PURPLE (property name)
};

// Property access
user.name              // 🟣 PURPLE
user.email             // 🟣 PURPLE
user.profile.avatar    // 🟣 PURPLE (both properties!)
```

### Variables vs Properties

```typescript
// Variables are white, properties are purple

const username = user.name;
//    ^^^^^^^^        ^^^^
//    ⚪ WHITE        🟣 PURPLE

const settings = config.database.connection;
//    ^^^^^^^^          ^^^^^^^^  ^^^^^^^^^^
//    ⚪ WHITE          🟣 PURPLE  🟣 PURPLE
```

### Arrow Functions

```typescript
// Parameters stay orange in arrow functions too!

const greet = (name: string, age: number) => {
  //           ^^^^           ^^^
  //           🟠 ORANGE      🟠 ORANGE
  
  console.log(`Hello ${name}, you are ${age}`);
  //                    ^^^^              ^^^
  //                    🟠 ORANGE         🟠 ORANGE
};
```

### Destructuring

```typescript
// Destructured parameters and properties

function Component({ title, onClose }: Props) {
  //                 ^^^^^  ^^^^^^^
  //                 🟠 ORANGE (params from destructure)
  
  return <div onClick={onClose}>{title}</div>;
  //                   ^^^^^^^   ^^^^^
  //                   🟠 ORANGE 🟠 ORANGE
}

const { user, settings } = state;
//      ^^^^  ^^^^^^^^
//      🟣 PURPLE (properties being destructured)
```

## ⚛️ React/JSX Examples

```tsx
// React component with enhanced colors

interface ButtonProps {
  label: string;     // 🟣 PURPLE
  onClick: () => void;  // 🟣 PURPLE
}

const Button = ({ label, onClick }: ButtonProps) => {
  //              ^^^^^  ^^^^^^^
  //              🟠 ORANGE (parameters)
  
  const [isHovered, setIsHovered] = useState(false);
  //     ^^^^^^^^^  ^^^^^^^^^^^^
  //     ⚪ WHITE   ⚪ WHITE (variables)
  
  return (
    <button
      onClick={onClick}
      //       ^^^^^^^
      //       🟠 ORANGE
      className={isHovered ? 'hover' : ''}
      //         ^^^^^^^^^
      //         ⚪ WHITE
    >
      {label}
      {/* ^^^^^ 🟠 ORANGE */}
    </button>
  );
};
```

## 🐍 Python Examples

```python
# Function parameters enhanced in Python too!

def process_data(ctx, items, options=None):
    #            ^^^  ^^^^^  ^^^^^^^
    #            🟠   🟠     🟠 ORANGE
    
    result = ctx.get_result(items)
    #        ^^^            ^^^^^
    #        🟠 ORANGE      🟠 ORANGE
    
    return result.data
    #             ^^^^
    #             🟣 PURPLE (property)
```

## 🔄 Before vs After Comparison

### BEFORE (Original Dracula)

```typescript
function getUserData(ctx: Context, userId: string) {
  const user = ctx.db.get(userId);
  return user.profile.settings;
}
// ❌ Problem: ctx, userId, user, profile, settings all same color
// Hard to distinguish parameters from properties from variables
```

### AFTER (Dracula Enhanced)

```typescript
function getUserData(ctx: Context, userId: string) {
  //                 ^^^           ^^^^^^
  //                 🟠 ORANGE     🟠 ORANGE
  
  const user = ctx.db.get(userId);
  //    ^^^^   ^^^          ^^^^^^
  //    ⚪     🟠 ORANGE    🟠 ORANGE
  
  return user.profile.settings;
  //          ^^^^^^^  ^^^^^^^^
  //          🟣 PURPLE 🟣 PURPLE
}
// ✅ Clear: Parameters orange, properties purple, variables white
// Easy to scan and understand code structure at a glance
```

## 🎯 Real-World Example

```typescript
// Complex real-world function with multiple concepts

async function updateUserProfile(
  ctx: Context,           // 🟠 ORANGE
  userId: string,         // 🟠 ORANGE
  updates: ProfileUpdate  // 🟠 ORANGE
) {
  // Validate
  const user = await ctx.db.users.get(userId);
  //    ^^^^              ^^^^^       ^^^^^^
  //    ⚪ WHITE          🟣 PURPLE   🟠 ORANGE
  
  if (!user) {
    throw new Error(`User ${userId} not found`);
    //                       ^^^^^^
    //                       🟠 ORANGE
  }
  
  // Update profile
  const updated = {
    ...user.profile,
    //     ^^^^^^^
    //     🟣 PURPLE
    ...updates
    // ^^^^^^^
    // 🟠 ORANGE
  };
  
  // Save
  await ctx.db.users.update(userId, updated);
  //    ^^^    ^^^^^                ^^^^^^
  //    🟠     🟣 PURPLE            ⚪ WHITE
  
  // Return updated data
  return {
    success: true,
    user: updated.profile
    //           ^^^^^^^
    //           🟣 PURPLE
  };
}
```

## 🔍 What You'll Notice

### Reading Code is Easier

1. **Scan for parameters**: Look for orange
2. **Find property access**: Look for purple  
3. **Identify variables**: They're the neutral white

### Code Structure Becomes Clear

```typescript
const result = api.fetch(endpoint).data.items;
//    ^^^^^^   ^^^       ^^^^^^^^  ^^^^  ^^^^^
//    ⚪       🟣        🟠        🟣    🟣
//    VARIABLE PROPERTY  PARAMETER PROP  PROP
```

### Refactoring is Safer

When you see orange, you know it's a parameter:
- Renaming it affects the function signature
- Changes might break calling code
- Need to check all usages

When you see purple, you know it's a property:
- Tied to object structure
- May need interface updates
- Could affect multiple components

## 💡 Pro Tips

### Use Color to Navigate

- **Orange trail** = Follow parameter through function
- **Purple dots** = Object property chain
- **White blocks** = Local variables and logic

### Debugging Benefits

```typescript
// Spot the bug faster:

function calculate(price: number, tax: number) {
  const total = price * price;  // 🐛 BUG!
  //                    ^^^^^
  //                    Should be 'tax' (orange) not 'price'
  return total;
}
```

### Code Review Benefits

Reviewers can quickly identify:
- Parameter usage patterns
- Property access chains
- Variable scope and lifecycle

## 🎨 Full Color Spectrum Example

```typescript
// Every color in action!

import { Database } from './db';  // 🟢 GREEN (import)

/**
 * Processes user data
 * @param ctx - The context  // 💬 GRAY (comment)
 */
async function processUser(      // 🟢 GREEN (function name)
  ctx: Context,                  // 🟠 ORANGE (parameter)
  userId: string                 // 🟠 ORANGE (parameter)
): Promise<Result> {             // 🔵 CYAN (type)
  
  const query = "SELECT * FROM users";  // 🟡 YELLOW (string)
  const id = 123;                       // 🟠 ORANGE (number)
  
  if (userId) {                  // 🌸 PINK (keyword)
    const user = await ctx.db.get(userId);
    //                         ^^^
    //                         🟣 PURPLE (property)
    
    return user.profile;         // 🌸 PINK (keyword)
    //          ^^^^^^^
    //          🟣 PURPLE (property)
  }
  
  throw new Error("Invalid");    // 🔴 RED (error/keyword new)
}
```

---

## 🚀 Get Started

Install Dracula Enhanced and experience these improvements yourself:

```bash
code --install-extension dracula-enhanced
```

Happy coding with better color clarity! 🦇✨