# rd-parse

rd-parse is a recursive descent parser for JavaScript, used in this repo to parse custom music notation. It allows for flexible grammar definitions and direct control over parsing logic.

## How Xenpaper Uses rd-parse

### 1. Basic Usage

rd-parse is imported and used to define the grammar for Xenpaper's text-based music notation.

#### Example

See `packages/xenpaper-ui/src/data/grammar.ts`:

```ts
import Parser, {All, Any, Optional, Star, Node} from 'rd-parse';

const grammar = All(/* ...grammar rules... */);
const parser = new Parser(grammar);
```

See `packages/xenpaper-ui/src/data/__tests__/grammar.test.ts`:

```ts
import Parser from 'rd-parse';
// ...tests for parsing music notation...
```

### 2. Grammar Definition and Parsing

rd-parse enables the creation of custom grammars for Xenpaper's notation, supporting features like chords, scales, and envelopes.

#### Example

See `packages/xenpaper-ui/src/data/grammar.ts`:

```ts
const grammar = All(
    // ...rules for notes, chords, envelopes, etc...
);
const parser = new Parser(grammar);

export function parse(input: string) {
    return parser.parse(input);
}
```

- The grammar is modular and can be extended for new notation features.
- Parsing is performed by calling `parser.parse(input)`.

### Instance Review and Recommendations

#### Grammar definition and parser creation (grammar.ts)
- **Assessment**: rd-parse enables flexible, extensible grammar for custom music notation. Migrating to PEG.js or another parser generator would add features but require a full rewrite.
- **Recommendation**: Keep rd-parse for current grammar. Consider PEG.js only if grammar complexity or debugging needs increase.

#### Usage in grammar.test.ts
- **Assessment**: Used for testing parser output. Tests are tightly coupled to rd-parse's API and grammar structure.
- **Recommendation**: Keep rd-parse for tests. If migrating grammar, update tests accordingly.

#### Usage in XenpaperGrammarParser (Xenpaper.tsx)
- **Assessment**: Used for parsing user input in the main app. Flexible and extensible for notation features.
- **Recommendation**: Keep rd-parse for this instance. Migration only justified if grammar or debugging needs change significantly.

## Critique and Alternatives

### Critique

While rd-parse provides flexibility for custom grammars, its use introduces some considerations:
- **Maintenance**: Custom grammars require ongoing updates and testing.
- **Learning Curve**: Contributors must understand recursive descent parsing and rd-parse's API.
- **Performance**: For very large inputs, custom parsers may be slower than optimized libraries.

### Alternatives

- **PEG.js**: Another parser generator for custom grammars, with more features and documentation.
- **Regular Expressions**: Sufficient for simple parsing tasks, but not for complex grammars.
- **Native JavaScript Parsing**: Manual parsing logic, but less maintainable for complex notation.

### Where rd-parse is Essential

In this codebase, rd-parse is essential for:
- Defining and parsing Xenpaper's flexible, extensible music notation.
- Supporting advanced features like chords, scales, and envelopes.

If the grammar grows in complexity, consider more feature-rich parser generators.

# Refactoring Options and Recommendation

## Your Options

1. **Continue Using rd-parse**
   - **Benefits**: Flexible, matches current grammar; easy to extend.
   - **Costs**: Maintenance burden; learning curve for new contributors.

2. **Migrate to PEG.js or Other Parser Generators**
   - **Benefits**: More features; better documentation; easier debugging.
   - **Costs**: Migration effort; may require grammar rewrite.

3. **Simplify Grammar for Small Projects**
   - **Benefits**: Less code; easier to maintain.
   - **Costs**: May lose advanced notation features.

## Recommendation

If your project relies on flexible, extensible notation, keeping rd-parse is recommended. For more features or easier onboarding, consider migrating to PEG.js or another parser generator. For simple notation, regular expressions or manual parsing may suffice.
