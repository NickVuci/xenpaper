# xenpaper (fork)

This is my fork of the original [https://dxinteractive.github.io/xenpaper/](https://dxinteractive.github.io/xenpaper/) project, a microtonal music sequencer and notation tool. The original repo is archived, but I intend to slowly pick away at improvements, refactoring, and new features as documented in `/VuciDocs`.

## Project Status

- **Forked and under slow, ongoing development.**
- **Original repo is archived; this fork is open for experimentation and gradual improvement.**

## Goals

- Address codebase messiness and disorganization, as outlined in `/VuciDocs/CleanUp`.
- Implement usability, functional, and developer experience improvements, as described in `/VuciDocs/improvements`.
- Document all changes, experiments, and rationale in `/VuciDocs`.

## What is Xenpaper?

Xenpaper is a text-based microtonal sequencer. It lets users write musical ideas in a custom text format and play them back, focusing on microtonal music (notes outside standard 12-tone equal temperament).

## Main Features

- Text-based music notation with support for chords, rests, holds, scales, and more.
- Microtonal support: custom scales, ratios, cents, EDO, etc.
- Live playback using Tone.js for synthesis.
- Pitch ruler visualization.
- Shareable links for tunes.

## Technologies

- React (UI)
- Styled-components (styling)
- Dendriform (state management)
- rd-parse (custom recursive descent parser)
- Tone.js (audio synthesis)
- Immer (immutable state updates)
- Jest (testing)

## Development Approach

I am using `/VuciDocs` to track, analyze, and plan all improvements and refactoring tasks. Progress will be incremental and experimental, with a focus on learning and code quality.

## Project Phases

1. **Refactor and Clean Up:**
   - Audit and refactor the codebase to improve structure, modularity, and maintainability.
   - Clean up the repository and remove dead code, duplication, and inconsistencies.

2. **Examine and Replace Experimental Patterns:**
   - Review all experimental libraries and patterns (e.g., craco, dendriform, styled-components, mosc abstraction).
   - Replace or refactor with more established and widely supported methods where appropriate.

3. **Build Additional Features and Functionality:**
   - Develop new features and enhancements on top of the refactored codebase.
   - Focus on usability, visualization, collaboration, and extensibility.
