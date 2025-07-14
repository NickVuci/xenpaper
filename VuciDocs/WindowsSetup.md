# Windows Setup Guide for Xenpaper

This document lists all known areas in the Xenpaper codebase and documentation where Unix/macOS commands or code need to be translated for Windows compatibility. Use this guide to ensure a smooth development experience on Windows.

---

## Status: ✅ All required changes for Windows compatibility have been completed.

---

## 1. Environment Variables in Scripts
- **Issue:** Unix-style environment variable setting (e.g., `VAR=value command`) does not work in Windows PowerShell or Command Prompt.
- **Solution:** Use `cross-env` in npm/yarn scripts.
- **Example:**
  - **Original:** `PUBLIC_URL="/xenpaper" DISABLE_ESLINT_PLUGIN=true NODE_OPTIONS=--openssl-legacy-provider craco start`
  - **Windows:** `cross-env PUBLIC_URL=/xenpaper DISABLE_ESLINT_PLUGIN=true NODE_OPTIONS=--openssl-legacy-provider craco start`
- **Location:** `packages/xenpaper-app/package.json` (scripts)
- **Status:** ✅ Updated and working

## 2. Shell Commands in Documentation
- **Issue:** Unix commands like `rm -rf`, `export VAR=...`, `cp`, etc. do not work in Windows.
- **Solution:** Use Windows equivalents or PowerShell commands.
- **Examples:**
  - `rm -rf node_modules` → `Remove-Item -Recurse -Force node_modules`
  - `export VAR=value` → `set VAR=value` (cmd) or `$env:VAR="value"` (PowerShell)
  - `cp src dest` → `Copy-Item src dest`
- **Location:** README.md, VuciDocs, and setup scripts
- **Status:** ✅ Scripts and docs updated

## 3. Path Separators
- **Issue:** Hardcoded `/` path separators may fail on Windows.
- **Solution:** Use Node's `path.join()` or `path.resolve()` for cross-platform paths.
- **Location:** Custom scripts and config files
- **Status:** ✅ No issues found in current codebase

## 4. Line Endings
- **Issue:** Windows uses CRLF (`\r\n`), Unix uses LF (`\n`).
- **Solution:** Use `.gitattributes` to normalize line endings if collaborating cross-platform.
- **Example:** Add `* text=auto` to `.gitattributes`.
- **Status:** ✅ No issues found; add if collaborating cross-platform

## 5. Additional Notes
- **Dependencies:** All major dependencies (React, craco, lerna, etc.) are cross-platform.
- **PowerShell vs. CMD:** Some commands differ between PowerShell and Command Prompt. Prefer PowerShell for scripting.
- **Yarn and Node:** Ensure both are installed and available in your PATH.
- **Status:** ✅ All dependencies and tools confirmed

---

**Summary:**
All required changes for Windows compatibility have been completed. Xenpaper should work smoothly on Windows. Always use `cross-env` for environment variables, translate shell commands in docs, and use Node APIs for paths. If you encounter new Unix-only commands, add their Windows equivalents to this guide.
