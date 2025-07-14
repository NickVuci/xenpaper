# Codebase Clean-Up & Refactoring Guide

This document identifies areas of messiness and disorganization in the Xenpaper codebase and provides actionable options for refactoring.

---

## Areas of Messiness & Disorganization

### 1. Monorepo Structure
- **Observation:** Multiple packages (`xenpaper-ui`, `xenpaper-app`, `mosc`, `sound-engine-tonejs`) with custom interdependencies. Some configs (like craco) are duplicated or scattered.
- **Refactoring Options:**
  - Consolidate shared configs (e.g., Babel, Webpack) into a root config.
  - Use Yarn Workspaces or PNPM for clearer dependency management.
  - Consider merging smaller packages if separation isn’t justified.

### 2. State Management
- **Observation:** Uses dendriform for all state, even simple booleans/numbers. This adds complexity for trivial state.
- **Refactoring Options:**
  - Use React’s `useState` or Context for simple state.
  - Reserve dendriform for deeply nested or collaborative state only.
  - Document state boundaries and rationale for each approach.

### 3. Custom Parsing Logic
- **Observation:** Custom recursive descent parser (`rd-parse`) and grammar files are tightly coupled to UI logic.
- **Refactoring Options:**
  - Move parsing logic to a dedicated package or module.
  - Write unit tests for parser and grammar.
  - Document grammar and parsing rules for maintainability.

### 4. Build & Config Files
- **Observation:** craco configs are complex and not well documented; environment variables are scattered.
- **Refactoring Options:**
  - Centralize build configs and document each override.
  - Remove unused or redundant config options.
  - Consider migrating to Vite or Next.js for simpler config.

### 5. Styling
- **Observation:** Uses styled-components, but styles may be scattered or inconsistent.
- **Refactoring Options:**
  - Standardize style patterns (e.g., theme provider, global styles).
  - Move styles to dedicated files or modules.
  - Remove unused styles.

### 6. Testing
- **Observation:** Jest is listed, but test coverage may be low or inconsistent.
- **Refactoring Options:**
  - Add/expand unit and integration tests, especially for parsing and playback.
  - Use code coverage tools to identify gaps.

### 7. Documentation
- **Observation:** Docs are fragmented; some experimental features are undocumented.
- **Refactoring Options:**
  - Centralize documentation in `/docs` or [`VuciDocs`](VuciDocs).
  - Add code comments and usage examples.
  - Document experimental patterns and rationale.

---

## General Refactoring Recommendations

1. **Audit and Remove Dead Code:** Identify unused files, components, and dependencies.
2. **Modularize Complex Logic:** Separate parsing, playback, and UI logic into clear modules.
3. **Standardize State Management:** Use the simplest tool for each state need.
4. **Improve Documentation:** Add README sections, code comments, and developer guides.
5. **Automate Linting and Formatting:** Use ESLint and Prettier for consistency.
6. **Consider Modern Alternatives:** Migrate to Vite/Next.js if possible for simpler build and config.

---

**Summary:**
The codebase is messy due to experimental patterns, scattered configs, and tightly coupled logic. Refactoring should focus on modularity, documentation, and using mainstream tools where possible, while retaining experimental features only where they are truly needed.
