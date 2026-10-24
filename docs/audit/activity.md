# 活動ログ

> 作業の時系列の記録。**追加のみ**で、過去の行は書き換えない。

| 日付 | 内容 | 証拠（コミット等） |
|---|---|---|
| 2026-10-19 | TEMPLATE_REPO の Agent 設定（`AGENTS.md` / `.agent/`）を取り込み、wsl-home 用に最適化（BASE-1）。`wsl-dotfiles` スキルを追加 | `c0ee132`、`e38a2d8` |
| 2026-10-19 | 配置方式を「chezmoi 設計参考の Bun + TypeScript 自前ツール」に決定（DESIGN-1） | `c8d04fc`、`69b8455` |
| 2026-10-19 | TEMPLATE_REPO 残り一式を取り込み docs 運用へ移行（BASE-2）。引っ越し・暗号化・CLI/TUI の機能要求も記録 | `a9c0f85`。`make check` PASS |
| 2026-10-25 | Dependency graph を有効化（ユーザー操作）し、BASE-2 を完了にした。PR はセッション権限維持のためマージせず継続利用する | PR #1 |
