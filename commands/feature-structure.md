---
name: feature-structure
description: Create feature-based folder structure with TypeScript path aliases
---

Create a feature-based folder structure for an Expo app with the following:

1. Create these directories:

   - src/features/ (for feature modules)
   - src/shared/components/
   - src/shared/ui/
   - src/shared/hooks/
   - src/shared/utils/
   - src/shared/types/

2. Update tsconfig.json to add these path aliases:

   - @components/_ → src/shared/components/_
   - @ui/_ → src/shared/ui/_
   - @hooks/_ → src/shared/hooks/_
   - @utils/_ → src/shared/utils/_
   - @types/_ → src/shared/types/_
   - @features/_ → src/features/_

3. Create index.ts barrel files in:

   - src/shared/components/
   - src/shared/ui/
   - src/shared/hooks/

4. Preserve all existing tsconfig.json settings, only add/update the baseUrl and paths.

Show me the final structure when done.
