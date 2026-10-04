# Writing & Sentence Checker

The checker is designed as a learner-focused, multi-layer writing assistant.

## Correction pipeline

1. **Context-aware local rules** — deterministic rules handle common spelling, contractions, modal verbs, articles, subject–verb agreement, capitalization, punctuation, repeated words and common learner constructions.
2. **LanguageTool (optional)** — an independent spelling/grammar pass is used when reachable from the server.
3. **OpenAI contextual review (optional)** — used for meaning-aware issues that deterministic rules cannot reliably decide.
4. **Conflict protection** — local safe corrections take priority. Overlapping remote corrections are suppressed so an external model cannot replace a precise correction with an unrelated phrase.
5. **Safe-fix protection** — AI findings are never automatically marked as safe fixes. Remote findings must reference an exact phrase from the submitted text and pass a plausibility check.
6. **Re-check after fixing** — applying safe fixes updates the editor and runs the checker again.

## Example

Input:

`W can do anything.`

Detection:

`W` → `We`

Corrected:

`We can do anything.`

The checker also handles lowercase `w` in the same grammatical context without producing a second contradictory capitalization warning.

## Important accuracy rule

No English checker can guarantee literal 100% correctness for every possible sentence because natural language depends on context, intended meaning, dialect and style. The system therefore separates **clear errors**, **context-dependent review items**, and **optional suggestions**, while restricting automatic fixes to high-confidence corrections.
