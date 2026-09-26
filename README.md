[日本語](README.ja.md) | **English**

# Sieve-Order v1.1.0

**AI Prompt Observation Engine**

*Sieve-Order is a tool for visualizing AI prompts. It outputs the observable structures contained in a prompt in receipt form.*

> Sieve-Order observes free-form AI prompts as orders in a deterministic, zero-dependency,
> explainable form, and returns the observation as a receipt for both humans and AI systems.

[Sieve](https://github.com/neguseatama/sieve-core) series is extended here into the domain of **AI order structure**.

> v1.0 finalized the boundary of what is observed and what is not observed.  
> v1.1 adds English surface vocabulary to the same observation model without adding semantic interpretation.

---

## 💡 Concept

A free-form prompt is treated like an order at a fast-food restaurant.

- **Order** — the free-form prompt written by the user
- **Menu** — the observable REQUEST / ACTION / TARGET vocabulary
- **Order slip** — the order structure observed from the input
- **Receipt** — the order slip plus the six-axis observation result

For example:

`Please check the document.`

is observed as:

```text
REQUEST = REQUEST
ACTION  = check
TARGET  = document
```

Japanese uses the same model:

`資料を確認してください。`

```text
REQUEST = REQUEST
ACTION  = 確認
TARGET  = 資料
```

REQUEST expressions are normalized into one set. They are not ranked by politeness, strength, goodness, or badness.

**The Observer does not complete missing parts or infer what the user meant.** It records only the menu elements and relations that are observable under the current rules.

---

## 📐 6-bit Observation Space

| Axis | Name | Observable surface |
|------|------|---------------------|
| H2 | REQUEST | Request / instruction surface |
| H3 | ACTION + TARGET | Explicit local surface relation |
| H4 | Instruction Hierarchy | Explicit instruction-hierarchy interference surface |
| H5 | External Rule Match | Match against an externally supplied rule expression |
| H6 | Obfuscation Surface | Invisible control-character / Base64-like surface pattern |
| H7 | External Reference | URL / file-reference surface pattern |

Mask notation: `H2H3H4H5H6H7` (for example, `110000`).

`0` does not prove that something is absent. It means that no evidence was observed under the current rules.

---

## 🍔 Menu

The minimum menu has three categories.

- **REQUEST** — Japanese and English request/instruction surface expressions.
- **ACTION** — a deliberately small fixed vocabulary of observable action words.
- **TARGET** — a deliberately small fixed vocabulary of observable target words.

The menu is not a semantic classifier. Only observed components are placed on the receipt; missing components are not completed.

### H3: local surface relation

H3 uses language-specific surface rules:

- Japanese: `TARGET + particle + ACTION`, such as `資料を確認`
- English: `ACTION + optional surface linker + TARGET`, such as `check the document`

H3 does not expand parallel targets or reconstruct semantic relations across multiple orders.

English H3 can therefore react to ordinary descriptive prose more readily than the corresponding Japanese surface rule. This is a documented property of the current lexical observation method, not a claim of semantic classification accuracy.

---

## 🧾 Receipts

The same `Observation` is projected into two representations:

1. **Human Receipt** — a human-readable receipt
2. **Machine Receipt** — structured data for AI or software

Both contain the same observation facts. The human representation does not add a judgment, and the machine representation does not hide or add an observation.

### Evidence Locations

When the original input is available, the Human Receipt can display existing Evidence `start`/`end` positions and nearby source context as `EVIDENCE LOCATIONS`. This is display-only navigation back to existing Evidence. It does not add an observation or interpret negation, quotation, intent, or execution scope.

---

## 🔍 H5 boundary

H5 observes only a match against an externally supplied rule expression.

For example, if the supplied rule is `credentials`,

`These are not credentials.`

still produces a lexical H5 match. This is not a conclusion that the text actually contains credentials.

---

## ⚠️ What is not observed

This version does not infer or classify:

- intent
- legality
- morality
- maliciousness
- truth of external claims
- model-specific token count
- H3 semantic relation expansion, including inferred relations for parallel TARGETs
- execution scope of quoted, example, or explanatory text
- semantic ACTION/TARGET pairing across multiple orders

These are explicit boundaries of the observation scope. They are not merely capabilities that have not been implemented yet.

---

## 🌐 Supported languages

Sieve-Order v1.1.0 supports exactly two surface-language sets:

- Japanese (`ja`)
- English (`en`)

The observer does not perform language identification or translation.

English morphology is intentionally not inferred. For example, the fixed menu item `check` does not automatically imply `checking` or `checked`.

---

## 🔥 Main features

- **6-bit observation space (H2-H7)**  
  Independent, deterministic observation of explicitly defined surface signals.
- **Zero dependency**  
  Python standard library only. Offline operation with no telemetry.
- **Deterministic**  
  The same input, rules, and configuration produce the same observation.
- **Explainable**  
  Evidence includes observable text and reproducible character positions.
- **Observation, not judgment**  
  The engine presents evidence and does not declare an order good, bad, legal, illegal, malicious, or safe.
- **Human Receipt / Machine Receipt**  
  Both are projections of the same `Observation`.
- **Japanese + English**  
  Exactly two supported lexical surface-language sets in v1.1.0.
- **Boundary-first evaluation**  
  Boundary cases are fixed as regression tests instead of optimizing real-world accuracy metrics.

---

## 📦 Installation

```bash
pip install .
```

The core implementation has no runtime dependency outside the Python standard library.

---

## 💻 Quick start

```bash
python -m sieve_order "Please check the document."
python -m sieve_order --json "Please check the document."
```

Japanese input remains supported:

```bash
python -m sieve_order "資料を確認してください。"
```

---

## 🔬 Tests

```bash
python -m unittest discover -s sieve_order/tests -v
```

The test suite checks deterministic behavior, receipt projection, language-specific boundaries, metadata consistency, and specification invariants. It is not a real-world accuracy benchmark.

---

## 📝 Changelog

See [CHANGELOG.md](CHANGELOG.md) for release details and [docs/V1_0_SPEC_CHECKLIST.md](docs/V1_0_SPEC_CHECKLIST.md) and [docs/V1_1_SPEC_CHECKLIST.md](docs/V1_1_SPEC_CHECKLIST.md) for the v1.0 and v1.1 observation-boundary checklists.

---

## 📄 License

MIT License. See [LICENSE](LICENSE).

---

## 👤 Author

**Kai IWASAKI**  
Email: `neguse.cat@gmail.com`

---
