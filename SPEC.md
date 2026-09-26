# Sieve-Order v1.1.0 Specification

## 1. Core model

A prompt is treated as an AI order.

`prompt -> observable order -> receipt`

The observable order uses a deliberately small menu with three categories:

- **REQUEST**: normalized request/instruction surface expressions. Japanese and English forms belong to language-specific request sets and are not ranked.
- **ACTION**: a fixed vocabulary of observable action words.
- **TARGET**: a fixed vocabulary of observable target words.

The supported surface-language sets are exactly Japanese and English. The menu is lexical. It does not claim to understand intent, semantics, legality, morality, or safety.

## 2. Menu and relation

The minimum menu is:

`MENU = { REQUEST, ACTION, TARGET }`

Each item can be observed independently. Missing items remain missing. No counterpart is inferred.

H3 records an explicitly observable **local ACTION/TARGET relation** using language-specific surface rules:

- Japanese: **TARGET + particle + ACTION**
- English: **ACTION + TARGET**

An ACTION or TARGET appearing alone does not create H3. H3 does not expand parallel targets or reconstruct semantic relations across multiple orders.

## 3. Observation function

`f(prompt, rules) = (H2,H3,H4,H5,H6,H7,Order,Metrics)`

## 4. Receipt invariance

Human and machine receipts MUST be derived from the same `Observation` object. They MUST NOT contain different observations.

## 5. Judgment boundary

The observer MUST NOT infer intent, legality, morality, maliciousness, truth of external claims, or model-specific token count.

The observer also deliberately does not assign semantic execution scope or reconstruct semantic order structure. In particular:

- **H3 local relation only**: H3 records only the explicitly observable local ACTION/TARGET relation under the supported language surface rules. It does not expand parallel targets into additional relations or infer that multiple targets belong to one action.
- **Quoted/explanatory text execution scope is not observed**: quoted text, example text, or text presented as material to explain is not classified as either an executable order or a non-executable order. Lexical evidence inside such text may still be observed.
- **Cross-order semantic pairing is not observed**: ACTION and TARGET occurrences are retained in input order, but the observer does not reconstruct semantic order units or pair every TARGET with an ACTION across multiple requests.

These are observation-scope boundaries, not claims that such structures are impossible to infer by another system.

## 6. H5

H5 reports only that the prompt matched an externally supplied rule expression. It does not interpret negation or context as a legal/moral/safety conclusion.

## 7. Determinism

Same prompt + same rules + same configuration => same observation.

The implementation does not depend on network access, randomness, external AI models, or time-dependent rules.

## 8. Evaluation

Tests are specification invariants and boundary checks, not evidence of real-world classification performance.

## 9. Receipt projection

A receipt is a projection of an `Observation`, not an independent judgment.

- Human Receipt MUST be derived only from the supplied `Observation`.
- Machine Receipt MUST contain the same observation data.
- Receipt metadata such as `JUDGMENT: NOT_PERFORMED` is protocol metadata, not an additional judgment.
- A receipt renderer MUST NOT infer missing order parts or add semantic conclusions.
- Human Receipt Evidence Locations are display-only context around existing Evidence.

## 10. v1.0 boundary checklist

The v1.0 observation boundary remains closed in v1.1.0:

- Deterministic observation is defined.
- Evidence locations are reproducible.
- Human and Machine Receipts are projections of the same Observation.
- Source context in Human Receipt is display-only.
- The implementation has no network or model dependency.
- REQUEST / ACTION / TARGET are explicitly defined.
- H3 is limited to explicit local relations; no semantic relation expansion is performed.
- Quoted, example, or explanatory text is not assigned execution scope.
- Cross-order semantic pairing is not reconstructed.
- Judgment and unobservable boundaries are explicit.

## 11. Language boundary

The v1.1.0 implementation supports exactly two lexical surface-language sets:

- Japanese (`ja`)
- English (`en`)

The observer does not perform language identification or translation.

English morphology is not inferred. A fixed menu item such as `check` does not automatically imply `checking` or `checked`.

English H3/H4 evidence can have lower discriminability from ordinary descriptive prose than the corresponding Japanese surface rules. This is a limitation of the lexical observation method, not a promise of future classification accuracy.

## 12. v1.1 boundary checklist

The v1.1 model preserves the v1.0 observation boundary and adds English surface coverage without changing the semantic scope:

- Deterministic observation is defined.
- Evidence locations are reproducible.
- Human and Machine Receipts are projections of the same Observation.
- Source context in Human Receipt is display-only.
- The implementation has no network or model dependency.
- REQUEST / ACTION / TARGET are explicitly defined for Japanese and English surface vocabulary.
- H3 is limited to explicit local language-specific relations; no semantic relation expansion is performed.
- Quoted, example, or explanatory text is not assigned execution scope.
- Cross-order semantic pairing is not reconstructed.
- Judgment and unobservable boundaries are explicit.
- Only Japanese and English surface-language sets are supported.
- English morphology is not inferred beyond fixed lexical menu items.

This checklist describes specification boundaries; it does not require additional semantic observation features.
