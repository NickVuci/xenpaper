# Build & Config Files

## Overview

This document analyzes build and configuration files in the Xenpaper codebase, focusing on craco and environment variables, and provides recommendations for refactoring.

## What to Examine
- craco config files
- Babel/Webpack configs
- Environment variable usage
- Redundancy and documentation

## Template for Analysis
- **Instance:** Config file/location
- **Analysis:** Description of the config issue
- **Recommendation:** Actionable steps for improvement

## Detailed Analysis

# Build & Config Files: Instance-by-Instance Analysis

## Overview
Build and configuration in Xenpaper relies on craco, Babel, Jest, and environment variables, with configs duplicated across packages.

## Instances & Analysis

### 1. craco.config.js
- **File:** `packages/xenpaper-app/craco.config.js`
- **Analysis:** Customizes Webpack aliases and includes multiple source directories for transpilation.
- **Problems:** Complex, not well documented. Hardcoded paths may break if structure changes.
- **Options:** Document config overrides. Use environment variables for paths if possible.
- **Recommendation:** Document and simplify config; consider migration to Vite/Next.js.

### 2. babel.config.js
- **Files:** `packages/xenpaper-ui/babel.config.js`, `packages/mosc/babel.config.js`
- **Analysis:** Nearly identical Babel configs in multiple packages.
- **Problems:** Duplication leads to maintenance overhead.
- **Options:** Move Babel config to root and reference in packages.
- **Recommendation:** Centralize Babel config.

### 3. jest.config.js
- **Files:** `packages/xenpaper-ui/jest.config.js`, `packages/mosc/jest.config.js`
- **Analysis:** Nearly identical Jest configs in multiple packages.
- **Problems:** Duplication and risk of config drift.
- **Options:** Move Jest config to root and reference in packages.
- **Recommendation:** Centralize Jest config.

### 4. Environment Variables
- **File:** `.env` in `xenpaper-app`
- **Analysis:** Used for build and runtime configuration.
- **Problems:** Scattered, not documented.
- **Options:** Document all environment variables and their usage.
- **Recommendation:** Centralize and document environment variables.

## Summary & Refactoring Recommendations
- Centralize and document build/config files.
- Remove duplication and simplify overrides.
- Consider migration to Vite/Next.js for simpler config.
