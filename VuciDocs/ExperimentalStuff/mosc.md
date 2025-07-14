# mosc

mosc is a custom abstraction for music/score logic in this repo. It provides types and functions for representing, processing, and converting musical data, especially for microtonal and experimental notation.

## How Xenpaper Uses mosc

### 1. Basic Usage

mosc defines core types for musical items, scores, and parameters, and is imported throughout the codebase for music processing.

#### Example

See `packages/mosc/src/mosc.ts`:

```ts
export type MoscNote = { /* ... */ };
export type MoscScore = { sequence: MoscItem[] };
export function scoreToMs(score: MoscScore): MoscScoreMs { /* ... */ }
// ...other types and functions...
```

See `packages/xenpaper-ui/src/Xenpaper.tsx`:

```tsx
import type { MoscScore } from "@xenpaper/mosc";
import { scoreToMs } from "@xenpaper/mosc";
// ...use MoscScore and scoreToMs to process and play music...
```

### Instance Review and Recommendations

#### MoscScore, MoscNoteMs, scoreToMs, centsToRatio, etc. (in mosc.ts and UI code)
- **Assessment**: These abstractions are tailored for microtonal and time-based music logic. They enable features not found in standard music libraries. Migrating to a conventional library would lose microtonal flexibility and require significant refactoring.
- **Recommendation**: Keep mosc for all core music logic. If interoperability or standardization becomes a priority, consider integrating with Tone.js or MIDI.js for playback, but retain mosc for notation and processing.

### 2. Advanced Usage and Integration

mosc supports advanced music processing, including microtonal notation, time conversion, and parameter handling. Its types and functions are used in UI components and data processing modules.

#### Example

See `packages/xenpaper-ui/src/PitchRuler.tsx`:

```tsx
import type { MoscNoteMs } from '@xenpaper/mosc';
import { centsToRatio } from '@xenpaper/mosc';

// Used for pitch visualization and color mapping:
const getGradientColorFromNote = (note: MoscNoteMs): string => { /* ... */ };
const getColorFromNoteProximity = (note: MoscNoteMs, proxNotes: MoscNoteMs[], threshold: number, hard: boolean): string => { /* ... */ };
```

See `packages/xenpaper-ui/src/data/process-grammar.ts`:

```ts
import { MoscScore, MoscItem } from '@xenpaper/mosc';
// Used to process parsed music data into playable scores
```

### Instance Review and Recommendations

#### Usage in PitchRuler.tsx and process-grammar.ts
- **Assessment**: Used for pitch visualization, color mapping, and score processing. These are tightly coupled to Xenpaper's custom notation and playback needs.
- **Recommendation**: Keep mosc for these instances. Migration would only be justified if the app's music logic becomes conventional and microtonal features are no longer needed.

## Critique and Alternatives

### Critique

While mosc provides a flexible abstraction for music logic, its use introduces some considerations:
- **Custom API**: New contributors must learn the custom types and functions.
- **Limited Reuse**: Being tailored for Xenpaper, mosc may not be reusable in other projects.
- **Testing and Maintenance**: Custom abstractions require thorough testing and ongoing maintenance.

### Alternatives

- **Standard Music Libraries**: Libraries like Tone.js or MIDI.js offer more conventional APIs but may lack microtonal support.
- **Direct Data Structures**: For simple projects, direct use of arrays/objects may suffice.

### Where mosc is Essential

In this codebase, mosc is essential for:
- Representing and processing microtonal and time-based music data.
- Converting between musical notation and playback formats.

If the project expands or needs interoperability, consider integrating with standard music libraries.

# Refactoring Options and Recommendation

## Your Options

1. **Continue Using mosc**
   - **Benefits**: Matches current code; supports microtonal and experimental needs.
   - **Costs**: Custom API; maintenance burden.

2. **Integrate with Standard Music Libraries**
   - **Benefits**: Easier onboarding; more features; better documentation.
   - **Costs**: May lack microtonal support; migration effort.

3. **Simplify Data Structures for Small Projects**
   - **Benefits**: Less code; easier to maintain.
   - **Costs**: May lose advanced features; less flexible for future growth.

## Recommendation

If your project relies on microtonal or experimental music logic, keeping mosc is recommended. For broader interoperability or easier onboarding, consider integrating with standard music libraries or simplifying data structures if advanced features are not needed.
