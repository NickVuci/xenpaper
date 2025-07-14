# Testing

## Overview

This document analyzes testing in the Xenpaper codebase, focusing on Jest usage and test coverage, and provides recommendations for refactoring.

## What to Examine
- Test files and coverage
- Unit and integration tests
- Use of code coverage tools

## Template for Analysis
- **Instance:** Test file/module
- **Analysis:** Description of the testing approach
- **Recommendation:** Actionable steps for improvement

## Detailed Analysis

# Testing: Instance-by-Instance Analysis

## Overview
Testing in Xenpaper uses Jest and Testing Library, with test files for core logic and parsing, but coverage is inconsistent.

## Instances & Analysis

### 1. Core Logic Tests
- **File:** `packages/mosc/src/__tests__/mosc.test.ts`
- **Analysis:** Tests for music logic functions (centsToRatio, scoreToMs, etc.).
- **Problems:** Good coverage for core functions, but may miss edge cases.
- **Options:** Expand tests for edge cases and error handling.
- **Recommendation:** Audit and expand core logic tests.

### 2. Grammar and Parsing Tests
- **Files:** `packages/xenpaper-ui/src/data/__tests__/grammar.test.ts`, `process-grammar.test.ts`
- **Analysis:** Large test files for grammar and score processing.
- **Problems:** Large, monolithic tests; unclear boundaries between features.
- **Options:** Split tests by feature and improve organization.
- **Recommendation:** Modularize and expand parsing tests.

### 3. Hook Tests
- **Files:** `hooks/__tests__/useHash.test.ts`, `useWindowLoaded.test.ts`
- **Analysis:** Tests for custom hooks (hashing, window load detection).
- **Problems:** Some hooks lack tests or have minimal coverage.
- **Options:** Add/expand tests for all custom hooks.
- **Recommendation:** Audit and expand hook tests.

## Summary & Refactoring Recommendations
- Audit and expand test coverage for all features.
- Modularize large test files by feature.
- Add/expand tests for custom hooks and edge cases.
