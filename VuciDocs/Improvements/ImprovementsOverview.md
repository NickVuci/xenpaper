# Improvements Overview

This document collects recommendations for improvements and additional functionality for Xenpaper, based on a thorough examination of the codebase and its current capabilities.

---

## Usability Improvements

1. **Enhanced Editor Experience**
   - Add syntax highlighting and error feedback for the custom notation.
   - Implement auto-completion for notation keywords and scales.
   - Provide inline documentation/tooltips for notation features.

2. **Better Visualization**
   - Expand the pitch ruler to show more detailed microtonal relationships.
   - Add a piano roll or grid view for easier editing and playback visualization.
   - Allow users to zoom and pan the visualization.

3. **Playback Controls**
   - Add tempo and playback speed controls.
   - Enable loop regions and playback from arbitrary positions.
   - Provide metronome and count-in options.

4. **Preset Management**
   - Allow users to save, load, and share tune presets.
   - Add a library of example tunes and scales for inspiration.

5. **Collaboration Features**
   - Implement real-time collaborative editing (multi-user).
   - Add version history and undo/redo across sessions.

6. **Accessibility**
   - Improve keyboard navigation and screen reader support.
   - Add high-contrast and large-font UI options.

---

## Functional Improvements

1. **Scale and Tuning Tools**
   - Add a scale editor for creating and modifying microtonal scales visually.
   - Support importing/exporting scales in popular formats (Scala, SCL, etc.).

2. **Audio Engine**
   - Allow users to select different synthesis engines or soundfonts.
   - Add support for MIDI export and import.
   - Enable advanced envelope and effects editing.

3. **Notation Extensions**
   - Support more advanced musical constructs (polyrhythms, tuplets, dynamics).
   - Add chord and harmony analysis tools.

4. **Mobile and Offline Support**
   - Make the UI responsive for mobile devices.
   - Add offline support for editing and playback.

---

## Codebase & Developer Experience

1. **Refactor for Modularity**
   - Separate parsing, playback, and UI logic into clear modules/packages.
   - Standardize state management (use dendriform only where needed).

2. **Improve Documentation**
   - Add a user manual and developer guide.
   - Document all experimental features and their rationale.

3. **Testing**
   - Increase test coverage, especially for parsing and playback.
   - Add integration tests for UI and audio engine.

4. **Modernize Build Tools**
   - Migrate to Vite or Next.js for faster builds and easier config.
   - Use Yarn Workspaces or PNPM for monorepo management.

---

**Summary:**
Xenpaper is a powerful microtonal sequencer, but usability, visualization, collaboration, and codebase maintainability can be improved. Focus on editor enhancements, visualization, collaboration, and modular code structure for the next phase of development.
