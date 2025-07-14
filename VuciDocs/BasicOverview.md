# BasicOverview

## What is Xenpaper?

Xenpaper is a text-based microtonal sequencer. It lets users write musical ideas in a custom text format and play them back, focusing on microtonal music (notes outside standard 12-tone equal temperament).

## Structure

- **Monorepo** managed by Lerna, with multiple packages in `packages/`.
- Main packages:
  - `xenpaper-ui`: React UI for editing, visualizing, and playing tunes.
  - `xenpaper-app`: App wrapper for deployment.
  - `mosc`: Likely core music/score logic.
  - `sound-engine-tonejs`: Sound engine using [Tone.js](https://tonejs.github.io/) for audio playback.

## Key Features

- **Text-based music notation**: Users type sequences like `0 4 7 12` for notes, with syntax for chords, rests, holds, scales, and more.
- **Microtonal support**: Custom scales, ratios, cents, EDO (equal divisions of octave), etc.
- **Live playback**: Uses Tone.js for synthesis.
- **Pitch ruler visualization**: Shows played notes and scales graphically.
- **Shareable links**: Tunes can be encoded in URLs for sharing.

## Technologies

- **React** (UI)
- **Styled-components** (styling)
- **Dendriform** (state management)
- **rd-parse** (custom recursive descent parser for music notation)
- **Tone.js** (audio synthesis)
- **Immer** (immutable state updates)
- **Jest** (testing)

## Status

- **Archived**: No longer maintained, but open for forking.
- **Experimental**: Codebase uses several experimental patterns and libraries.

## How it works

1. **User writes tune** in a text area using Xenpaper's notation.
2. **Parser** ([`grammar.ts`](../packages/xenpaper-ui/src/data/grammar.ts)) converts text to an AST.
3. **Processor** ([`process-grammar.ts`](../packages/xenpaper-ui/src/data/process-grammar.ts)) translates AST to a score for playback.
4. **Sound engine** ([`sound-engine-tonejs.ts`](../packages/sound-engine-tonejs/src/sound-engine-tonejs.ts)) plays the score.
5. **UI** (`xenpaper-ui`) provides editing, visualization, and sharing features.

## Example tune

```
0 4 7 12
(env:0158)
{4:5:6}
```

- Notes, envelope settings, and custom scale.

## Summary

Xenpaper is a microtonal music sequencer with a custom text notation, real-time playback, and visualization, built as a React monorepo with a focus on experimental and open-source development. For more details, see [`README.md`](../README.md) and the main UI code in [`packages/xenpaper-ui/src/Xenpaper.tsx`](../packages/xenpaper-ui/src/Xenpaper.tsx).
