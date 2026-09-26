# Observation Notes v1.1.0

Sieve-Order v1.1.0 adds English lexical surface rules to the existing observation model.
This document records exploratory observations; it is not a ground-truth evaluation set.

## English H3 surface behavior

English H3 uses a local lexical `ACTION + TARGET` surface relation. Because English normally expresses object relations through word order rather than a dedicated object particle, ordinary descriptive prose can produce the same local surface evidence as an apparent AI order.

Examples:

- `I will delete the file and then generate a report tomorrow.` -> H3 evidence can observe `delete the file`; `generate a report` is not reconstructed when no supported TARGET is observed for that local surface.
- `The report will get the data and display the result on the dashboard automatically.` -> H3 can observe `get the data` and `display the result` even though the sentence is descriptive prose rather than an AI order.

This is not treated as a semantic classification error. The observer is recording the local surface relation it was specified to observe.

## English H4 surface behavior

Some English H4 expressions are ordinary language rather than specialized instruction-hierarchy terminology.

Examples:

- `Please don't forget the instructions for tomorrow's assembly.` -> H4 lexical evidence can observe `forget the instructions`.
- `We should prioritize following the safety instructions during the drill.` -> H4 lexical evidence can observe `prioritize following the safety instructions`.

These examples show that English H4 has lower discriminability from ordinary prose than the corresponding Japanese surface rules. The project does not compensate by adding semantic intent classification.

## Boundary decision

The v1.1.0 implementation keeps these observations as-is. The limitation is documented in `SPEC.md` as a language-specific property of the lexical observation method.

The corpus exists to make such behavior visible and reproducible, not to optimize accuracy against a hidden ground truth.
