# State Management

## Overview

This document analyzes state management in the Xenpaper codebase, focusing on the use of dendriform and other state tools, and provides recommendations for refactoring.

## What to Examine
- Usage of dendriform, React `useState`, and Context
- State boundaries and rationale
- Complexity vs. simplicity in state management

## Template for Analysis
- **Instance:** File/component
- **Analysis:** Description of the state management approach
- **Recommendation:** Actionable steps for improvement

## Detailed Analysis

# State Management: Instance-by-Instance Analysis

## Overview
State in Xenpaper is managed primarily with dendriform, but also with React hooks. This enables granular updates but adds complexity for simple state.

## Instances & Analysis

### 1. tuneForm (useDendriform<TuneForm>)
- **File:** `packages/xenpaper-ui/src/Xenpaper.tsx`
- **Analysis:** Deeply nested, frequently updated state. Dendriform is best here.
- **Problems:** None; dendriform is appropriate for this use case.
- **Options:** Migrate to Redux for more ecosystem support, but would add boilerplate.
- **Recommendation:** Keep dendriform.

### 2. parsedForm (useDendriform<Parsed>)
- **File:** `packages/xenpaper-ui/src/Xenpaper.tsx`
- **Analysis:** Derived, reactive state. Dendriform is well-suited.
- **Problems:** None; dendriform is appropriate.
- **Options:** Redux could work but adds complexity; Context/useState not reactive enough.
- **Recommendation:** Keep dendriform.

### 3. playing (useDendriform<boolean>)
- **File:** `packages/xenpaper-ui/src/Xenpaper.tsx`
- **Analysis:** Simple boolean state. Could use useState or Context for simplicity unless granular subscriptions are needed.
- **Problems:** Overkill for simple state.
- **Options:** Migrate to useState/Context.
- **Recommendation:** Migration to useState/Context is reasonable.

### 4. selectedLine (useDendriform<number>)
- **File:** `packages/xenpaper-ui/src/Xenpaper.tsx`
- **Analysis:** Simple numeric state. Could use useState or Context unless granular subscriptions are needed.
- **Problems:** Overkill for simple state.
- **Options:** Migrate to useState/Context.
- **Recommendation:** Migration to useState/Context is reasonable.

### 5. looping (useDendriform<boolean>)
- **File:** `packages/xenpaper-ui/src/Xenpaper.tsx`
- **Analysis:** Simple boolean state. Could use useState or Context.
- **Problems:** Overkill for simple state.
- **Options:** Migrate to useState/Context.
- **Recommendation:** Migration to useState/Context is reasonable.

### 6. RulerState (useDendriform<RulerState>)
- **File:** `packages/xenpaper-ui/src/PitchRuler.tsx`
- **Analysis:** Complex, nested state for pitch visualization. Dendriform is best for granular updates.
- **Problems:** None; dendriform is appropriate.
- **Options:** Redux or MobX could work, but dendriform is more granular.
- **Recommendation:** Keep dendriform.

### 7. Types and Props (Dendriform<TuneForm>, etc.)
- **File:** Various
- **Analysis:** If state is managed by dendriform, types are appropriate. If migrating simple state, update types accordingly.
- **Problems:** Types may be overcomplicated for simple state.
- **Options:** Update types if migrating to another method.
- **Recommendation:** Keep dendriform types where used; update if migrating to another method.

## Summary & Refactoring Recommendations
- Use dendriform for deeply nested or collaborative state.
- Use useState/Context for simple state.
- Update types if migrating simple state.
