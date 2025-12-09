---
name: setup-jest
description: Install testing libraries
---

Install testing libraries:

1. Install testing libraries:

```bash
   bunx expo install jest-expo jest @types/jest @testing-library/react-native --dev
```

2. Update package.json:
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

3. Confirm setup is complete with testing ready to go.
