---
name: setup-nativewind
description: Install and setup NativeWind (Tailwind CSS for React Native) in Expo project
args:
  - name: package_manager
    description: Package manager to use (bun/npm/pnpm/yarn)
    required: true
---

Install and configure NativeWind v4 with Tailwind CSS in your Expo project:

## 1. Validate Package Manager

Verify the package manager argument is one of: bun, npm, pnpm, or yarn.
If invalid, show error and exit.

## 2. Install NativeWind and Dependencies

Install nativewind, tailwindcss, and prettier-plugin-tailwindcss:

**For bun:**

```bash
bun add nativewind
bun add -d tailwindcss@^3.4.17 prettier-plugin-tailwindcss@^0.5.11
```

**For npm:**

```bash
npm install nativewind
npm install --save-dev tailwindcss@^3.4.17 prettier-plugin-tailwindcss@^0.5.11
```

**For pnpm:**

```bash
pnpm add nativewind
pnpm add -D tailwindcss@^3.4.17 prettier-plugin-tailwindcss@^0.5.11
```

**For yarn:**

```bash
yarn add nativewind
yarn add -D tailwindcss@^3.4.17 prettier-plugin-tailwindcss@^0.5.11
```

**Note:** Skip installing react-native-reanimated and react-native-safe-area-context as they are already bundled with Expo SDK.

## 3. Initialize Tailwind CSS

Run Tailwind CSS initialization using the appropriate package runner:

**For bun:**

```bash
bunx tailwindcss init
```

**For npm:**

```bash
npx tailwindcss init
```

**For pnpm:**

```bash
pnpm dlx tailwindcss init
```

**For yarn:**

```bash
yarn dlx tailwindcss init
```

This creates a `tailwind.config.js` file.

## 4. Configure Tailwind CSS

Update `tailwind.config.js` with the following content:

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./app/**/*.{js,jsx,ts,tsx}",
    "./src/**/*.{js,jsx,ts,tsx}",
    "./components/**/*.{js,jsx,ts,tsx}",
  ],
  presets: [require("nativewind/preset")],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

## 5. Create Global CSS File

Create `global.css` in the root directory with Tailwind directives:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

## 6. Update Babel Config

Modify `babel.config.js` to add the NativeWind preset:

```javascript
module.exports = function (api) {
  api.cache(true);
  return {
    presets: [
      ["babel-preset-expo", { jsxImportSource: "nativewind" }],
      "nativewind/babel",
    ],
  };
};
```

**Important:** Preserve any existing plugins in babel.config.js (like module-resolver if present).

## 7. Create or Update Metro Config

Create or update `metro.config.js` in the root:

```javascript
const { getDefaultConfig } = require("expo/metro-config");
const { withNativeWind } = require("nativewind/metro");

const config = getDefaultConfig(__dirname);

module.exports = withNativeWind(config, { input: "./global.css" });
```

## 8. Update app.json

Add Metro bundler configuration for web in `app.json`:

```json
{
  "expo": {
    "web": {
      "bundler": "metro"
    }
  }
}
```

**Important:** Only add the "web" section if it doesn't exist. If "web" already exists, only add or update the "bundler" property.

## 9. Import Global CSS

Check if using Expo Router or standard Expo structure:

**For Expo Router (app/\_layout.tsx):**

```typescript
import "../global.css";

// Rest of your layout code
```

**For standard Expo (App.tsx or App.js):**

```typescript
import "./global.css";

// Rest of your app code
```

Add the import at the very top of the file, before any other imports.

## 10. Setup TypeScript Support (if using TypeScript)

Create `nativewind-env.d.ts` in the root directory:

```typescript
/// <reference types="nativewind/types" />
```

**Important:** Do NOT name this file:

- `nativewind.d.ts`
- The same as any existing file or folder
- The same as any node_modules folder name

## 11. Update Prettier Config (if exists)

If `.prettierrc` exists, add the Tailwind plugin:

```json
{
  "plugins": ["prettier-plugin-tailwindcss"]
}
```

## 12. Verify Installation

Show a test component example to verify NativeWind is working:

```typescript
import { View, Text } from "react-native";

export default function TestScreen() {
  return (
    <View className="flex-1 items-center justify-center bg-white">
      <Text className="text-xl font-bold text-blue-500">
        NativeWind is working! 🎉
      </Text>
    </View>
  );
}
```

Confirm the following:

- NativeWind and Tailwind CSS installed
- tailwind.config.js created and configured
- global.css created with directives
- babel.config.js updated with NativeWind presets
- metro.config.js configured with withNativeWind
- app.json updated with Metro bundler
- global.css imported in root component
- TypeScript types configured (if applicable)
- Prettier plugin added (if applicable)

## Usage Notes

After setup, you can use Tailwind utility classes via the `className` prop:

```typescript
<View className="flex-1 bg-gray-100 p-4">
  <Text className="text-2xl font-bold text-gray-800">Hello</Text>
  <Pressable className="bg-blue-500 py-3 px-6 rounded-lg active:bg-blue-600">
    <Text className="text-white text-center font-semibold">Press me</Text>
  </Pressable>
</View>
```

## Rules

- DO NOT install react-native-reanimated or react-native-safe-area-context (already in Expo SDK)
- DO NOT overwrite existing babel.config.js plugins, merge with existing config
- DO NOT replace entire app.json, only add/update necessary fields
- ALWAYS import global.css at the top of the root component
- ALWAYS use the correct package runner (bunx, npx, pnpm dlx, yarn dlx)
- If metro.config.js exists, merge withNativeWind wrapper with existing config
