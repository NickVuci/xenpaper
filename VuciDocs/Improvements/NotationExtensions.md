# Notation Extensions

## Implementation Ideas
- **Polyrhythms, tuplets, and complex time signatures:**
  - Extend parser and UI to support advanced rhythmic constructs.
  - Visualize rhythms in piano roll and score views.
  - **Ease:** Moderate to hard; parser and UI changes required.
  - **Issues:** Backward compatibility, user education.

- **Dynamic markings and articulation symbols:**
  - Add support for dynamics (pp, ff, crescendos) and articulations (staccato, legato).
  - Allow entry via notation and UI controls.
  - **Ease:** Moderate; notation and playback logic needed.
  - **Issues:** Mapping to playback engine, notation complexity.

- **Chord and harmony analysis:**
  - Analyze and visualize chord structures and harmonic relationships.
  - Provide feedback and suggestions for harmony.
  - **Ease:** Moderate; music theory algorithms required.
  - **Issues:** Accuracy of analysis, visualization clarity.

- **Custom note attributes:**
  - Allow users to set velocity, articulation, and color for notes.
  - Visualize attributes in score and playback.
  - **Ease:** Easy to moderate; UI and data model changes.
  - **Issues:** Data model complexity, UI clutter.

- **Notation export:**
  - Export scores to MusicXML, LilyPond, or PDF formats.
  - Add export options to UI and backend.
  - **Ease:** Moderate; libraries exist for export.
  - **Issues:** Format compatibility, completeness of export.

## Summary
Notation extensions will make Xenpaper more expressive and compatible with other music tools, but require parser, UI, and data model updates.
