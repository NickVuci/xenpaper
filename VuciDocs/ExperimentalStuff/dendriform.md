# dendriform

dendriform is an experimental state management library designed for complex, nested, and collaborative editing scenarios. It provides granular control over state updates and is less common than mainstream solutions like Redux or MobX. Its use in this repo reflects a willingness to try new approaches for managing application state.

## How Xenpaper Uses dendriform

### 1. Basic Usage

The repo uses dendriform to manage UI state in several components, especially in `Xenpaper.tsx` and `PitchRuler.tsx`.

#### Example

See `packages/xenpaper-ui/src/Xenpaper.tsx`:

```tsx
import { useDendriform, useInput } from "dendriform";
import type { Dendriform } from "dendriform";

// ...existing code...
const tuneForm = useDendriform<TuneForm>();
const parsedForm = useDendriform<Parsed>(() => parse(tuneForm.value.tune));
const playing = useDendriform<boolean>(false);
const selectedLine = useDendriform<number>(0);
const looping = useDendriform<boolean>(false);
// ...existing code...
```

See `packages/xenpaper-ui/src/PitchRuler.tsx`:

```tsx
import {useDendriform, useCheckbox, useInput} from 'dendriform';
import type {Dendriform} from 'dendriform';

// ...existing code...
return useDendriform<RulerState>(() => {
    // ...state logic...
});
// ...existing code...
```

### 2. Advanced Usage and Patterns

dendriform enables advanced state management patterns, such as nested state and collaborative editing. In Xenpaper, dendriform forms are used to manage complex, nested UI state and propagate changes efficiently.

#### Example

See `packages/xenpaper-ui/src/Xenpaper.tsx`:

```tsx
// ...existing code...
// dendriforms with application state
const tuneForm = useDendriform<TuneForm>({
    tune: "",
    // ...other fields...
});
// tuneForm can be deeply nested and updated granularly
// ...existing code...
```

// Dendriform also allows for branching and merging state, which is useful for collaborative editing scenarios (not fully implemented in this repo, but supported by the library).

### 3. Integration with React and UI

dendriform integrates with React via hooks, allowing components to subscribe to granular state changes and update efficiently. This is seen throughout Xenpaper's UI code.

#### Example

See `packages/xenpaper-ui/src/Xenpaper.tsx`:

```tsx
// ...existing code...
const playing = useDendriform<boolean>(false);
const selectedLine = useDendriform<number>(0);

// Used directly in JSX:
<Button onClick={() => playing.set(true)}>Play</Button>
<LineSelector value={selectedLine.value} onChange={selectedLine.set} />
// ...existing code...
```

## Critique and Alternatives

### Critique

While dendriform provides powerful and granular state management, its use introduces some risks:
- **Learning Curve**: Dendriform is less common than Redux or MobX, so new contributors may need time to learn its API and patterns.
- **Community Support**: Fewer resources and examples are available compared to mainstream state libraries.
- **Complexity**: Advanced features like branching and merging state may be overkill for simpler apps.

### Alternatives

- **Redux**: Well-documented, widely used, and integrates with many tools. May require more boilerplate for nested state.
- **MobX**: Simple and reactive, good for complex state but less granular than dendriform.
- **React Context/State**: Sufficient for simple state needs, but not as powerful for nested or collaborative scenarios.

### Where dendriform is Essential

In this codebase, dendriform is essential for:
- Managing deeply nested and granular UI state (e.g., tuneForm, parsedForm).
- Enabling efficient updates and subscriptions in complex components.

If the project grows in collaborative editing or nested state complexity, dendriform's advanced features may become even more valuable. For simpler state needs, mainstream libraries may be easier to maintain.

# Refactoring Options and Recommendation

## Your Options

1. **Continue Using dendriform**
   - **Benefits**: Supports granular, nested, and potentially collaborative state; matches current code structure.
   - **Costs**: Learning curve for new contributors; less community support.

2. **Migrate to Redux or MobX**
   - **Benefits**: Well-documented, widely used, easier onboarding; strong ecosystem.
   - **Costs**: May require refactoring nested state logic; possible loss of some advanced features.

3. **Use React Context/State for Simpler Needs**
   - **Benefits**: Minimal setup; easy for small apps.
   - **Costs**: Not suitable for deeply nested or collaborative state.

## Recommendation

If your app relies on deeply nested, granular, or collaborative state, dendriform is a good fit. For simpler state needs or if onboarding new contributors is a priority, consider migrating to Redux or MobX. If you expect future growth in collaborative features, dendriform's advanced capabilities may be worth keeping.

## Instance Review and Recommendations

#### tuneForm (useDendriform<TuneForm>)
- **Assessment**: Deeply nested, frequently updated state. Dendriform is best here. Migration to Redux would add boilerplate; Context/useState would be insufficient.
- **Recommendation**: Keep dendriform.

#### parsedForm (useDendriform<Parsed>)
- **Assessment**: Derived, reactive state. Dendriform is well-suited. Redux could work but adds complexity; Context/useState not reactive enough.
- **Recommendation**: Keep dendriform.

#### playing (useDendriform<boolean>)
- **Assessment**: Simple boolean state. Could use useState or Context for simplicity unless granular subscriptions are needed.
- **Recommendation**: Migration to useState/Context is reasonable.

#### selectedLine (useDendriform<number>)
- **Assessment**: Simple numeric state. Could use useState or Context unless granular subscriptions are needed.
- **Recommendation**: Migration to useState/Context is reasonable.

#### looping (useDendriform<boolean>)
- **Assessment**: Simple boolean state. Could use useState or Context.
- **Recommendation**: Migration to useState/Context is reasonable.

#### RulerState (useDendriform<RulerState>) in PitchRuler.tsx
- **Assessment**: Complex, nested state for pitch visualization. Dendriform is best for granular updates.
- **Recommendation**: Keep dendriform.

#### Types and Props (Dendriform<TuneForm>, etc.)
- **Assessment**: If state is managed by dendriform, types are appropriate. If migrating simple state, update types accordingly.
- **Recommendation**: Keep dendriform types where used; update if migrating to another method.
