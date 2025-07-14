# Styling

## Overview

This document analyzes styling in the Xenpaper codebase, focusing on styled-components and style organization, and provides recommendations for refactoring.

## What to Examine
- Usage of styled-components
- Style consistency and organization
- Unused or redundant styles

## Template for Analysis
- **Instance:** File/component
- **Analysis:** Description of the styling approach
- **Recommendation:** Actionable steps for improvement

## Detailed Analysis

# Styling: Instance-by-Instance Analysis

## Overview
Styling in Xenpaper is managed with styled-components and styled-system, but styles are scattered and sometimes inconsistent.

## Instances & Analysis

### 1. Global Styles
- **File:** `packages/xenpaper-ui/src/AppWrapper.tsx`
- **Analysis:** Uses `createGlobalStyle` for CSS resets and global styles.
- **Problems:** Global styles are defined in JS, which may be harder to maintain for large projects.
- **Options:** Move global styles to a dedicated file/module.
- **Recommendation:** Keep for now, but consider modularizing if styles grow.

### 2. Component Styles
- **Files:** `component/ErrorMessage.tsx`, `IconButton.tsx`, `Text.tsx`, etc.
- **Analysis:** Uses styled-components for encapsulated styles and keyframes for animation.
- **Problems:** Styles are scattered across many files; some duplication in animation logic.
- **Options:** Standardize style patterns and move common styles to shared modules.
- **Recommendation:** Modularize and deduplicate styles.

### 3. Layout Styles
- **Files:** `layout/Layout.ts`, `TextWrapper.ts`, `Wrapper.tsx`
- **Analysis:** Uses styled-system for responsive and theme-based layout.
- **Problems:** Some props and theme usage may be inconsistent.
- **Options:** Standardize theme usage and document layout props.
- **Recommendation:** Audit and standardize layout styles.

### 4. Styled-System Usage
- **Files:** `Text.tsx`, `Layout.ts`, etc.
- **Analysis:** Integrates styled-system for utility props.
- **Problems:** May be overkill for simple components; increases bundle size.
- **Options:** Use styled-system only where needed.
- **Recommendation:** Audit usage and remove from simple components.

## Summary & Refactoring Recommendations
- Modularize and deduplicate styles.
- Standardize theme and layout usage.
- Audit styled-system usage and remove where unnecessary.
