---
name: new-expo-app
description: Create a new Expo app with testing setup and open it in Windsurf
args:
  - name: app_name
    description: Name of the Expo app
    required: true
---

Create a new Expo app with testing libraries:

1. Navigate to `/Users/ahsantariq/developer/expo`

2. Create a new Expo app:

```bash
   cd /Users/ahsantariq/developer/expo
   npx create-expo-app {{app_name}}
```

3. Install testing libraries:

```bash
   cd {{app_name}}
   npx expo install jest-expo jest @types/jest --dev
   npx expo install @testing-library/react-native --dev
```

4. Update package.json:
   - Add `"test": "jest"` to the scripts section
   - Add jest configuration:

```json
   "jest": {
     "preset": "jest-expo",
     "transformIgnorePatterns": [
       "node_modules/(?!((jest-)?react-native|@react-native(-community)?)|expo(nent)?|@expo(nent)?/.*|@expo-google-fonts/.*|react-navigation|@react-navigation/.*|@unimodules/.*|unimodules|sentry-expo|native-base|react-native-svg)"
     ]
   }
```

5. Open in Windsurf:

```bash
   surf .
```

6. Confirm setup is complete with testing ready to go.
