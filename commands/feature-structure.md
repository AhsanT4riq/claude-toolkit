---
name: feature-structure
description: Create feature-based folder structure with TypeScript path aliases for Expo Router with NativeWind
---

Create a feature-based folder structure optimized for Expo Router with NativeWind and Zustand/Valtio:

## 1. Create Directory Structure

Create these directories:

```
src/
├── features/           # Feature modules (auth, profile, home, etc.)
└── shared/
    ├── components/     # Shared RN components (Card, List, etc.)
    ├── ui/            # UI primitives (Button, Input, Text, etc.)
    ├── hooks/         # Custom React hooks (useKeyboard, useTheme, etc.)
    ├── utils/         # Utility functions (storage, validation, etc.)
    ├── types/         # TypeScript types/interfaces
    ├── constants/     # Colors, spacing, dimensions, config
    ├── services/      # API clients, analytics, notifications
    └── store/         # Zustand/Valtio stores

app/                   # Expo Router file-based routing (already exists)
assets/               # Images, fonts (already exists in root)
```

Commands:

```bash
mkdir -p src/features
mkdir -p src/shared/{components,ui,hooks,utils,types,constants,services,store}
```

## 2. Update tsconfig.json

Add these path aliases while preserving existing Expo settings:

```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@components/*": ["src/shared/components/*"],
      "@ui/*": ["src/shared/ui/*"],
      "@hooks/*": ["src/shared/hooks/*"],
      "@utils/*": ["src/shared/utils/*"],
      "@types/*": ["src/shared/types/*"],
      "@constants/*": ["src/shared/constants/*"],
      "@services/*": ["src/shared/services/*"],
      "@store/*": ["src/shared/store/*"],
      "@features/*": ["src/features/*"]
    }
  }
}
```

**Note:** Expo SDK 50+ supports path aliases natively. Just add them to tsconfig.json and restart your dev server.

## 3. Create Barrel Export Files

**src/shared/components/index.ts:**

```typescript
// Export shared RN components here
```

**src/shared/ui/index.ts:**

```typescript
// Export UI primitives here
```

**src/shared/hooks/index.ts:**

```typescript
// Export custom React Native hooks here
```

**src/shared/utils/index.ts:**

```typescript
// Export utility functions here
```

**src/shared/constants/index.ts:**

```typescript
// Export constants here
```

**src/shared/services/index.ts:**

```typescript
// Export services here
```

**src/shared/store/index.ts:**

```typescript
// Export Zustand/Valtio stores here
```

**src/shared/types/index.ts:**

```typescript
// Global type definitions
```

## 4. Verify Setup

Show the complete directory tree and confirm:

- All directories created
- tsconfig.json updated with path aliases
- All barrel files created
- Dev server restarted

## Important Notes

- **Screens go in `app/` folder** - Expo Router file-based routing
- **Features export components, hooks, and stores** - Not screens
- **Use NativeWind classes** - className prop for styling
- **Store in features or shared** - Feature stores in features/, global stores in shared/store/
- **Assets in root** - Use existing assets/ folder in project root
- **Native path alias support** - Expo SDK 50+ handles this without babel-plugin-module-resolver

## Rules

- DO NOT create screens in features/ folder
- DO NOT create styles/ folder
- DO NOT create src/assets/ folder
- DO NOT install NativeWind packages
- DO NOT install babel-plugin-module-resolver (not needed in SDK 50+)
- DO NOT modify existing tsconfig.json compiler options except baseUrl and paths
- DO NOT delete any existing files
- ALWAYS restart dev server after updating tsconfig.json
