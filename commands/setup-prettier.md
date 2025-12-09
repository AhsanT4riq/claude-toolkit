---
name: setup-prettier
description: Configure ESLint & Prettier for code linting and formatting
args:
  - name: package_manager
    description: Package manager to use (bun/npm/pnpm/yarn)
    required: true
---

Configure ESLint and Prettier for code formatting and linting:

## 1. Validate Package Manager

Verify the package manager argument is one of: bun, npm, pnpm, or yarn.
If invalid, show error and exit.

## 2. Install Prettier

Install Prettier as a dev dependency using the specified package manager:

**For bun:**

```bash
bun add -d prettier
```

**For npm:**

```bash
npm install --save-dev prettier
```

**For pnpm:**

```bash
pnpm add -D prettier
```

**For yarn:**

```bash
yarn add -D prettier
```

## 3. Update package.json Scripts

Add these scripts to package.json (preserve existing scripts):

```json
{
  "scripts": {
    "lint": "eslint .",
    "lint:fix": "eslint . --fix",
    "format": "prettier --write ."
  }
}
```

## 4. Create .prettierrc

Create `.prettierrc` file in the root with these rules:

```json
{
  "semi": true,
  "trailingComma": "es5",
  "singleQuote": true,
  "printWidth": 100,
  "tabWidth": 2,
  "useTabs": false,
  "arrowParens": "avoid",
  "endOfLine": "lf",
  "bracketSpacing": true,
  "jsxSingleQuote": false,
  "quoteProps": "as-needed"
}
```

## 5. Create .prettierignore

Create `.prettierignore` file to exclude certain directories:

```
node_modules/
.expo/
.expo-shared/
dist/
build/
coverage/
*.lock
package-lock.json
yarn.lock
pnpm-lock.yaml
bun.lockb
.next/
.turbo/
android/
ios/
```

## 6. Update eslint.config.js

Check if `eslint.config.js` exists. If it exists, add the custom rules section. If it doesn't exist, inform the user.

Add these custom rules to the existing eslint.config.js:

```javascript
// Custom rules
{
  rules: {
    // React rules
    'react/jsx-filename-extension': ['warn', { extensions: ['.tsx', '.jsx'] }],
    'react/prop-types': 'off',
    // Import ordering & validation
    'import/order': [
      'error',
      {
        groups: [
          ['builtin', 'external'],
          'internal',
          ['parent', 'sibling', 'index'],
        ],
        pathGroups: [
          {
            pattern: 'react',
            group: 'external',
            position: 'before',
          },
          {
            pattern: 'react-native',
            group: 'external',
            position: 'before',
          },
          {
            pattern: 'expo-*',
            group: 'external',
            position: 'after',
          },
          {
            pattern: '@components/**',
            group: 'internal',
            position: 'before',
          },
          {
            pattern: '@/**',
            group: 'internal',
            position: 'after',
          },
        ],
        pathGroupsExcludedImportTypes: ['react', 'react-native'],
        'newlines-between': 'always',
        alphabetize: { order: 'asc', caseInsensitive: true },
      },
    ],
    'import/first': 'error',
    'import/newline-after-import': 'error',
    'import/no-duplicates': 'error',
  },
}
```

**Import Order Structure:**

1. React and React Native (at the very top)
2. Expo and other third-party/external packages
3. Internal modules (@components, @ui, @hooks, @utils, @types, @constants, @services, @store, @features)
4. Local relative imports (./, ../)

**Important:** Add this as a new object in the config array, don't replace existing rules.

## 7. Format All Files

Run Prettier on the entire codebase using the appropriate command for the package manager:

**For bun:**

```bash
bun run format
```

**For npm:**

```bash
npm run format
```

**For pnpm:**

```bash
pnpm run format
```

**For yarn:**

```bash
yarn format
```

## 8. Verify Setup

Confirm the following:

- Prettier installed successfully
- package.json scripts added (lint, lint:fix, format)
- .prettierrc created with rules
- .prettierignore created
- eslint.config.js updated with custom rules
- All files formatted

## Example Import Order

After setup, imports should look like this:

```typescript
import React, { useState } from "react";
import { View, Text, Pressable } from "react-native";

import { Stack } from "expo-router";
import { StatusBar } from "expo-status-bar";
import { SomeThirdPartyLib } from "some-package";

import { Button } from "@ui/Button";
import { Card } from "@components/Card";
import { useAuth } from "@hooks/useAuth";
import { formatDate } from "@utils/date";
import { User } from "@types/common";
import { COLORS } from "@constants";
import { apiClient } from "@services/api";
import { useAuthStore } from "@store/authStore";
import { LoginScreen } from "@features/auth";

import { localHelper } from "./helper";
import styles from "./styles";
```

## Rules

- DO NOT overwrite existing eslint.config.js, only append the custom rules
- DO NOT replace existing package.json scripts, only add new ones
- DO NOT format files if there are syntax errors
- DO NOT install eslint-plugin-import (comes with Expo SDK)
- ALWAYS use the specified package manager argument
- If eslint.config.js doesn't exist, inform user and skip that step
