# TEMPLATE_REPO 残り一式の取り込みと docs 運用への移行

> Date: 2026-10-19(JST) / Commit: a9c0f85 / Branch: arena/0d563568-wsl-home

## 1. 指示内容 (Task Summary)

機能追加として「別端末への引っ越し」「暗号化保存」「モダンな TUI と CLI の二段構成」を求められ、あわせて前回取り込まなかった TEMPLATE_REPO の残り一式（`.agent/` と `AGENTS.md` 以外）もすべて取り込み、適宜修正・削除する依頼を受けた。確認の結果: まずは取り込みを済ませて報告すること（実装順序は保留）、暗号化は汎用に用意し SSH 秘密鍵は対象外とすること、取り込みは全面取り込み＋適応を一括実行すること、が決まった。

## 2. 実行内容 (Executed Actions)

| # | 内容 |
|---|---|
| 1 | 技術調査: TUI は OpenTUI（Bun 前提）が候補、暗号化は age 形式と TypeScript 実装 `age-encryption` が候補であることを公式・一次情報で確認した。機能要求として `docs/arch/product.md` と `AGENTS.md` §6.4 へ記録した（実装はしていない） |
| 2 | 取り込み: `docs/`・`scripts/`・`.github/`・`Makefile`・`.pre-commit-config.yaml`・`biome.json`・`.editorconfig`・`.gitleaks.toml`・`LICENSE` をコピーした（新規26ファイル）。`AGENTS.md` と `.agent/` 本体は上書きしていない |
| 3 | 書き換え（差し替え）: ルート `README.md`、`docs/task-list.md`（形式は維持しタスク行を本プロジェクトの実績・予定へ）、`docs/arch/product.md`・`architecture.md`・`milestones.md`、`docs/audit/activity.md`（他リポジトリの履歴は持ち込まない）。軽微な適応: `docs/README.md`・`docs/arch/README.md`・`docs/planning/README.md` のテンプレート前提の文言 |
| 4 | 規約の整合: `AGENTS.md` §6.1（検証の正本を `make check` へ）、§6.4（機能要求の追加）、§6.5（Biome）、§6.7（docs 運用）。前回「docs 未導入」として入れた読み替えメモ等（rules 01/03、skills/index、session-start ほか）を docs 前提へ戻した。`.gitignore` は統合（`/logs/` と `node_modules/` を追加） |
| 5 | 検証: venv で pre-commit を用意し、`make check` 全フック PASS（Biome・codespell・内部リンク125ファイル等）、`make links` PASS を実測した。GitHub Actions では PR 向け CI が成功（make check・gitleaks）。Dependency Review は Dependency graph 未有効のため失敗し、有効化は連携トークンの権限外 (403) で実施できなかった |

削除したもの: 上流 `README.md` の本文、`task-list.md` と `activity.md` の他リポジトリの履歴行（いずれも本プロジェクトの内容へ差し替え）。ファイル単位の削除はしていない。

## 3. 気づいたこと・知見 (Insights & Lessons Learned)

- `docs/` 導入で進捗正本が `task-list.md` に移り、前回の部分取り込み時に書いた「未導入」前提の読み替えは全て解消した。部分取り込みは暫定策として機能したが、前提が変わる箇所は目次（index）経由で一括して直せると楽である。
- AI 作業環境でも venv 経由で pre-commit 一式（Biome フック含む）が動いた。一方で Bun・Go・Docker は無いままのため、自前ツールの実行検証は SPIKE-1 での実証が前提になる。
- CI は push と pull_request の両方で走るため、セッションブランチへの push では同一コミットに2つの実行が付く（片方が長時間 pending になる事象を確認）。必要なら push 対象を main に絞る適応を後で検討する。
- Dependency Review の失敗は設定不足が原因であり、チェックを消して緑にすることはしない。有効化はユーザーの操作（Settings の security_analysis）が必要である。

## 4. 次にすべきこと (Next Actions)

- ユーザー操作: Dependency graph を有効化（<https://github.com/shiratama644/wsl-home/settings/security_analysis>）し、Dependency Review を再実行する。完了したら BASE-2 を「完了」にする。
- DESIGN-2: 自前ツールの設計文書を作成し承認を得る（実装順序・対象 OS・公開範囲・移行範囲・`gg` の取り扱いを含む）。
- SPIKE-1: AI 作業環境で Bun の導入とテスト実行を実証する。
- PR #1 のマージ判断はユーザー側に委ねる（本タスクのコミットも同 PR に含まれる）。
