# Custom Parsing Logic

## Overview

This document analyzes the custom parsing logic in the Xenpaper codebase, focusing on `rd-parse` and grammar files, and provides recommendations for refactoring.

## What to Examine
- Parser implementation and coupling to UI
- Grammar documentation and maintainability
- Test coverage for parsing logic

## Template for Analysis
- **Instance:** File/module
- **Analysis:** Description of the parsing logic
- **Recommendation:** Actionable steps for improvement

## Detailed Analysis

# Custom Parsing Logic: Instance-by-Instance Analysis

## Overview
Xenpaper uses a custom recursive descent parser (`rd-parse`) and grammar files to convert user input into an AST and score for playback. This enables flexible notation but can be tightly coupled to UI logic.

## Instances & Analysis

### 1. grammar.ts
- **File:** `packages/xenpaper-ui/src/data/grammar.ts`
- **Analysis:** Implements grammar rules using `rd-parse`. Defines node types, delimiters, and parsing logic.
- **Problems:** Grammar is complex and not fully documented. Coupling to UI types may hinder maintainability.
- **Options:** Move grammar to a dedicated package/module. Add documentation for grammar rules.
- **Recommendation:** Decouple grammar from UI and document rules.

### 2. process-grammar.ts
- **File:** `packages/xenpaper-ui/src/data/process-grammar.ts`
- **Analysis:** Translates AST to score for playback. Handles conversion of notation to musical events.
- **Problems:** Large file, complex logic, limited test coverage.
- **Options:** Split into smaller modules. Add/expand unit tests.
- **Recommendation:** Modularize and test thoroughly.

### 3. Parser Usage in UI
- **File:** `packages/xenpaper-ui/src/Xenpaper.tsx`
- **Analysis:** UI directly invokes parser and processes results for playback and visualization.
- **Problems:** Tight coupling between parsing and UI logic.
- **Options:** Move parsing to a service layer or dedicated module.
- **Recommendation:** Decouple parsing from UI for maintainability.

### 4. Tests
- **Files:** `packages/xenpaper-ui/src/data/__tests__/grammar.test.ts`, `process-grammar.test.ts`
- **Analysis:** Tests exist for grammar and processing, but coverage may be incomplete.
- **Problems:** Large test files, unclear coverage boundaries.
- **Options:** Expand and organize tests by feature.
- **Recommendation:** Improve test coverage and organization.

## Summary & Refactoring Recommendations
- Decouple parsing logic from UI.
- Document grammar rules and parsing flow.
- Modularize large files and expand tests.
