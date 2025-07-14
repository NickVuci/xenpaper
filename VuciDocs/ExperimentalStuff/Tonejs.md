# Tone.js

Tone.js is a Web Audio framework for creating interactive music in the browser. In Xenpaper, it is used for real-time synthesis and playback of microtonal music.

## How Xenpaper Uses Tone.js

### 1. Basic Usage

Tone.js is imported and used to create synthesizers, manage transport, and schedule musical events.

#### Example

See `packages/sound-engine-tonejs/src/sound-engine-tonejs.ts`:

```ts
import * as Tone from 'tone';

synth = new Tone.PolySynth(Tone.Synth, { /* ...synth options... */ }).chain(Tone.Destination);

await Tone.start();
Tone.Transport.start();
Tone.Transport.stop();
Tone.Transport.cancel();
```

### 2. Advanced Usage and Integration

Tone.js is used to manage transport, looping, and scheduling of notes for playback. This enables real-time synthesis and flexible control over musical timing.

#### Example

See `packages/sound-engine-tonejs/src/sound-engine-tonejs.ts`:

```ts
Tone.Transport.loop = loop;
Tone.Transport.loopStart = ms * 0.001;
Tone.Transport.loopEnd = (ms === 0 ? this._endMs : ms) * 0.001;
Tone.Transport.cancel(); // clear previous notes
// ...add new notes to transport...
```

- Transport controls allow for starting, stopping, and looping playback.
- Notes are scheduled for precise timing and microtonal playback.

## Critique and Alternatives

### Critique

While Tone.js enables powerful browser-based synthesis, its use introduces some considerations:
- **Performance**: Complex scheduling and synthesis can impact browser performance.
- **Microtonal Support**: Tone.js is flexible, but microtonal features require custom logic.
- **Learning Curve**: Contributors must learn Tone.js's API and audio concepts.

### Alternatives

- **Web Audio API**: Direct use for maximum control, but more verbose and complex.
- **MIDI.js**: For MIDI playback, but less flexible for synthesis.
- **Other Synth Libraries**: May offer different features or performance tradeoffs.

### Where Tone.js is Essential

In this codebase, Tone.js is essential for:
- Real-time synthesis and playback in the browser.
- Flexible transport and scheduling for microtonal music.

If performance or feature needs change, consider alternatives or deeper integration with Web Audio API.

# Refactoring Options and Recommendation

## Your Options

1. **Continue Using Tone.js**
   - **Benefits**: Matches current code; supports real-time synthesis and flexible scheduling.
   - **Costs**: Learning curve; performance limits for complex projects.

2. **Integrate with Web Audio API Directly**
   - **Benefits**: Maximum control; can optimize for performance and features.
   - **Costs**: More verbose; harder to maintain.

3. **Switch to Other Synth Libraries or MIDI.js**
   - **Benefits**: May offer different features or easier MIDI integration.
   - **Costs**: May lose synthesis flexibility; migration effort.


## Instance-by-Instance Review and Recommendations

### File: `packages/sound-engine-tonejs/src/sound-engine-tonejs.ts`

**Instances of Tone.js usage:**

- `import * as Tone from 'tone';` — Essential for all Tone.js features.
- `synth = new Tone.PolySynth(Tone.Synth, {...}).chain(Tone.Destination);` — Polyphonic synth creation and output routing. Recommended for flexible synthesis; keep as-is unless you need lower-level control or performance optimization.
- `Tone.Transport` (state, loop, loopStart, loopEnd, seconds, start, stop, cancel, schedule, on): Used for playback control, looping, scheduling notes and parameter changes, and event handling. This is the core of real-time scheduling and playback in Xenpaper.
    - **Recommendation:** Tone.Transport is well-suited for this use case. Migrating to Web Audio API would require significant custom scheduling logic and is not recommended unless you need advanced performance tuning or features Tone.js cannot provide.
- `Tone.start()`: Required to unlock audio context in browsers. Keep as-is.
- `this.synth.triggerAttackRelease(...)`: Used for note playback with microtonal frequencies. Tone.js supports this well; keep unless you need more advanced synthesis features.
- Parameter scheduling (oscillator/envelope changes): Tone.js allows dynamic changes, but timing is not sample-accurate for parameter changes. If you need sample-accurate automation, consider Web Audio API, but for most musical use cases, Tone.js is sufficient.

**Summary of Recommendations:**

- For all current usages in `sound-engine-tonejs.ts`, Tone.js is the best fit given the requirements for real-time synthesis, flexible scheduling, and microtonal support. Migration to Web Audio API or another library is only recommended if you encounter performance bottlenecks or need features not supported by Tone.js.

## Recommendation

If your app relies on real-time synthesis and flexible scheduling, Tone.js is a good fit. For advanced performance or custom features, consider integrating with Web Audio API or other libraries as needed.
