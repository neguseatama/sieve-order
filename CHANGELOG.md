# v1.1.0

- Finalized the project name as **Sieve-Order**, following the Sieve ecosystem naming convention of `Sieve` + one English word.
- Renamed the Python distribution and import package from the provisional `sieve-prompt-observer` / `sieve_prompt` names to `sieve-order` / `sieve_order`.
- Added deterministic English surface vocabulary alongside the existing Japanese vocabulary.
- Extended REQUEST observation with English request surfaces such as `please`, `could you`, `would you`, and `can you`.
- Added English ACTION/TARGET menu items while keeping the menu intentionally small.
- Extended H3 with the English local surface relation `ACTION + TARGET`; Japanese remains `TARGET + particle + ACTION`.
- Extended H4 and H7 with English instruction-hierarchy and file-reference surface patterns.
- Preserved the v1.0 judgment and unobservable boundaries; no semantic interpretation was added.
- Declared Japanese and English as the only supported surface-language sets.
- Added English boundary and receipt regression tests.
- Added an English exploration section to `examples/order_corpus.md`, including ordinary descriptive prose that can trigger lexical H3/H4 evidence.
- Documented the language-specific boundary that English H3/H4 evidence can be less discriminative from ordinary descriptive prose than the corresponding Japanese surface rules.
- Added `README.md` as the primary English-language project README; retained `README.ja.md`.
- Aligned the README opening copy with the Sieve ecosystem style: **AI Prompt Observation Engine** / **AIプロンプト観測エンジン**, with the receipt-form visualization description.
- Added MIT `LICENSE` and author/contact metadata.

# v1.0.0

- READMEの「観測外」をSPECのv1.0境界と同期。
- README/SPECの観測外境界の整合性を回帰テストで固定。
- 観測モデルの仕様境界を確定。
- H3を明示的な局所関係に限定し、意味的な関係展開を行わないことを正式化。
- 引用・例文・説明対象テキストに実行スコープを割り当てないことを正式化。
- 複数注文にまたがる意味的なACTION/TARGET対応付けを復元しないことを正式化。
- v1.0仕様チェックリストを実装・テストスイートと対応付け。
- 観測ロジックの変更なし。

# v0.9.2

- H3の局所関係限定、引用・説明対象の実行スコープ非観測、複数注文の意味的対応付け非観測をSPEC.mdに明文化。
- v1.0仕様チェックリストを追加。
- 観測ロジックは変更せず、既存の観測境界を仕様として閉じた。

# v0.9.1

- Human Receipt に `EVIDENCE LOCATIONS` を追加。
- H3等の既存Evidenceについて、入力文字列が渡された場合のみ元位置と周辺文脈を表示。
- 文脈表示はProjectionであり、新しい観測・否定解釈・引用解釈を追加しない。
- CLIはHuman Receipt生成時に元入力を渡す。
- Machine ReceiptとObservationの構造は変更しない。
- 配布メタデータと文書バージョンの整合性を回帰テストで固定。
- Evidence context radius を名前付き定数 `EVIDENCE_CONTEXT_RADIUS` として明示。

# Changelog

## v0.9.0
- Human Receipt に `OBSERVED RELATIONS` を追加。
- 既存のH3 Evidenceのみを表示し、新しい関係推論は行わない。
- 複数Evidenceを入力順で表示する。

## v0.8.1
- REQUESTの `して` を文末表現として観測し、`確認して、...` のような接続表現をREQUESTとして誤観測しないよう境界を明確化。
- ACTION / TARGETのメニュー抽出を入力中の出現順に保持。
- 重複する語彙が入れ子になる場合は、長いメニュー項目を優先（例: `認証情報` を `情報` と分割しない）。
- 上記の境界を回帰テストとして固定。
- 配布メタデータのバージョンを `0.8.1` に更新。

## v0.8.0
- Formalized Human Receipt / Machine Receipt as projections of the same Observation.
- Machine Receipt now wraps the unchanged observation under `observation`.
- Added a regression test for receipt projection invariance.
- Removed generated `__pycache__` files from the distribution.

## v0.6.2
- Restored executable package files in the release archive.
- Added lexical menu extraction for ACTION and TARGET independently.
- Preserved H3 as evidence of an observable TARGET + particle + ACTION relation.
- Added `python -m sieve_order` CLI for human and machine receipts.
- Missing menu parts remain absent; no semantic completion is performed.

## v0.5.0
- 「注文・メニュー・レシート」を実装モデルとして正式化。
- REQUEST表現を単一集合 `REQUEST` に正規化。
- ACTION / TARGETを注文構造として実装。
- `Order` を `Observation` に内包。
- Human Receipt と Machine Receipt を同一Observationから生成。
- README / SPECを注文モデル中心に更新。
- 10件の仕様・境界テストを実装。

## v0.4.1
- H2 を個別の文末表現ではなく REQUEST 集合として整理。
- H3 を ACTION + TARGET の注文構造として明示。
- `Order` 構造を追加。
- 人間とAIに共有するレシート生成 `make_receipt()` を追加。
- H5 はルール照合のみを行い、否定や善悪を意味判断しないことを回帰テスト化。
- 6軸独立性・境界・依頼表現集合・レシートをテスト。
