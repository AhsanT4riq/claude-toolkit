---
description: Create a UI Component in `src/shared/ui/`
argument-hint: Component name | Component summary
---

## Context

Parse $ARGUMENTS to get the following values:

- [name]: Component name from $ARGUMENTS (in PascalCase, e.g., "Button", "Card", "Badge")
- [summary]: Component summary from $ARGUMENTS

## Project Standards

Reference the existing UI components structure:

- Location: `src/shared/ui/[name]/`
- Each component has three files:
  - `[name].tsx` - Component implementation
  - `[name].test.tsx` - Unit tests
  - `index.ts` - Barrel export

Styling guidelines:

- Use **NativeWind 4** (Tailwind CSS for React Native) for styling
- Reference theme colors from `src/shared/theme/colors.ts`
- Support theme-aware styling (light/dark mode)
- Use consistent spacing and sizing scales

## Task

Create a complete, production-ready UI component:

1. **Component Implementation** (`[name]/[name].tsx`):

   - Create a functional component named [name]
   - Use TypeScript with proper prop types
   - Support the standard variants: primary, secondary, success, error, warning, info
   - Make component composable and reusable
   - Include JSDoc comments for props
   - Ensure accessibility with ARIA attributes where applicable
   - Support NativeWind className styling

2. **Component API**:

   - Define a clear props interface (e.g., `[name]Props`)
   - Include size variants (sm, md, lg) if applicable
   - Support disabled state if interactive
   - Allow custom className override via `className` prop
   - Include children prop for composable content

3. **Barrel Export** (`[name]/index.ts`):

   - Export the component as default and named export
   - Export the props type

4. **Testing** (`[name]/[name].test.tsx`):

   - Test all variants (primary, secondary, success, error, warning, info)
   - Test size variations if applicable
   - Test interactive states (pressed, disabled, focused)
   - Test accessibility features (ARIA labels, keyboard navigation)
   - Use React Native Testing Library
   - Aim for >80% code coverage
   - Include snapshot tests for UI consistency

5. **Update Main Index**:
   - Add the new component to `src/shared/ui/index.ts`

## Implementation Checklist

- [ ] Component accepts variant prop and applies correct styling
- [ ] Component is accessible (WCAG AA compliant)
- [ ] Component works in both light and dark themes
- [ ] TypeScript types are properly defined
- [ ] All test suites pass
- [ ] Code coverage is adequate
- [ ] Barrel export is configured correctly
- [ ] Main UI index is updated with new export
- [ ] Component follows existing code patterns in the project

## Rules

- Use functional components only
- Always use TypeScript
- Reference existing components for style patterns
- Do NOT add unnecessary dependencies
- Do NOT break existing components or exports
- Ensure tests pass before completing: `bun run test`
- Run linting and formatting: `bun run lint:fix && bun run format`
