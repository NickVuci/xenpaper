# Monorepo Structure

## Overview

This document analyzes the monorepo structure of the Xenpaper codebase, identifies areas of messiness and disorganization, and provides detailed recommendations for refactoring.

## What to Examine
- Package organization in `/packages`
- Shared configuration files (Babel, Webpack, craco, etc.)
- Dependency management (Lerna, Yarn Workspaces)
- Inter-package dependencies and code sharing

## Template for Analysis
- **Instance:** File or config location
- **Analysis:** Description of the issue or pattern
- **Recommendation:** Actionable steps for improvement

## Detailed Analysis

# Monorepo Structure: Instance-by-Instance Analysis

## Overview
The Xenpaper codebase is organized as a monorepo using Lerna and Yarn Workspaces, with multiple packages in `/packages`. This structure enables code sharing but introduces complexity and duplication.

## Instances & Analysis

### 1. Root Monorepo Configs
- **File:** `lerna.json`, `package.json`
- **Analysis:**
    - Lerna is used for package management, with independent versioning and Yarn as the npm client.
    - Workspaces are defined for all packages, with some nohoist rules.
    - Scripts for test, lint, build, and bootstrap are defined at the root.
- **Problems:**
    - No central place for shared devDependencies (e.g., Babel, Jest configs duplicated in packages).
    - No explicit documentation of workspace boundaries or dependency flow.
- **Options:**
    - Move shared devDependencies to root `package.json`.
    - Add documentation for workspace/package boundaries.
- **Recommendation:**
    - Centralize devDependencies and document workspace structure.

### 2. Package Organization
- **Files:** `packages/xenpaper-ui`, `packages/xenpaper-app`, `packages/mosc`, `packages/sound-engine-tonejs`
- **Analysis:**
    - Each package has its own `package.json`, source folder, and (for most) Babel/Jest config.
    - Inter-package dependencies are managed via workspace versions (e.g., `@xenpaper/mosc`, `@xenpaper/sound-engine-tonejs`).
- **Problems:**
    - Some packages (e.g., `xenpaper-ui`) depend on others, but dependency flow is not documented.
    - Config files (Babel, Jest) are duplicated across packages.
    - No clear separation between UI, core logic, and sound engine.
- **Options:**
    - Document inter-package dependencies and intended boundaries.
    - Merge packages if separation is not justified.
    - Move shared configs to root or use tools like Nx for better management.
- **Recommendation:**
    - Document package boundaries and dependency flow. Consider merging packages or using Nx if scaling up.

### 3. Shared Config Files
- **Files:** `babel.config.js`, `jest.config.js` in multiple packages
- **Analysis:**
    - Babel and Jest configs are nearly identical in `xenpaper-ui` and `mosc`.
- **Problems:**
    - Duplication leads to maintenance overhead and risk of config drift.
- **Options:**
    - Move Babel/Jest configs to root and reference them in each package.
    - Use a tool like Nx or Turborepo for shared config management.
- **Recommendation:**
    - Centralize configs at the root and reference them in packages.

### 4. Inter-Package Imports
- **Files:** Source files in `xenpaper-ui` import from `mosc` and `sound-engine-tonejs`.
- **Analysis:**
    - Imports are direct and rely on workspace resolution.
- **Problems:**
    - No explicit documentation of which packages are intended to be public APIs vs. internal.
- **Options:**
    - Document public vs. internal packages.
    - Use TypeScript project references for clearer boundaries.
- **Recommendation:**
    - Document API boundaries and use TypeScript project references if possible.

## Summary & Refactoring Recommendations
- Centralize shared configs and devDependencies.
- Document package boundaries and dependency flow.
- Merge packages if separation is not justified.
- Use Nx or Turborepo for better monorepo management if scaling up.
