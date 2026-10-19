# TEMPLATE_REPO の Agent 設定取り込みと wsl-home 向け最適化

> Date: 2026-10-19(JST) / Commit: c0ee132 / Branch: arena/0d563568-wsl-home

## 1. 指示内容 (Task Summary)

出力形式などを決めるため、`shiratama644/TEMPLATE_REPO` の `.agents/`・`AGENTS.md`・`CLAUDE.md`・`.claude/` を本リポジトリへ取り込み、必要に応じてスキルや設定を本リポジトリ用に最適化する。取り込み前に事実確認と選択肢の確認を行い、ユーザーが次を承認した: (1) `.agents/` は上流に無いため正本の `.agent/` で再現する (2) 指定範囲のみ取り込み最適化まで行う（`docs/`・`Makefile` 等は取り込まない） (3) スキル44件は全保持し wsl-home 固有スキルを1件追加する (4) `.gitignore` 等の安全設定を dotfiles 向けに強化する。

## 2. 実行内容 (Executed Actions)

| # | 内容 |
|---|---|
| 1 | 上流 `TEMPLATE_REPO`（commit `267d9d0` に固定）から `.agent/` と `AGENTS.md` を実行権つきでコピーし、`CLAUDE.md -> AGENTS.md` / `.claude -> .agent` の symlink を再現した。上流の履歴ログ1件は本リポジトリの事実記録にならないため持ち込まなかった |
| 2 | `AGENTS.md` の冒頭注記と §6 を wsl-home 用に記入（環境の区別・検証コマンド・未決事項リスト等）。§8 のスキル件数を45件に更新した |
| 3 | `.agent/skills/project-overview/SKILL.md` を wsl-home の全体像に書き換え、引き継ぎ知識を新規スキル `.agent/skills/wsl-dotfiles/SKILL.md` に集約し、`skills/index.md` へ登録した |
| 4 | `rules/project-template.md` を §6 と揃えて記入。`rules/01`・`03` に `docs/` 未導入時の読み替えメモを追加し、`rules/04` と `hooks/post_edit_verify.sh` の秘密ファイル検出を秘密鍵等へ拡張した |
| 5 | `.agent/settings.json` に秘密鍵の読み取り拒否と構文チェック系の許可を追加し、`.gitignore` を新規作成した（秘密鍵・`.env`・履歴・個人設定の除外） |
| 6 | 検証: `sh -n`（フック4件）/ `settings.json` 妥当性 / symlink 解決 / スキル frontmatter 45件 / フック動作（force push ブロック等）/ 秘密検出の負荷テスト（ダミー `.env` を stage して検出を確認後、除去）/ 入口文書の内部リンク / `git diff --cached --check` がすべて PASS。上流ファイル1件の行末空白1つを最小修正した |

変更規模: コミット `c0ee132` で 130 files, +15,478 行（大半は上流の無改変コピー。内容を調整した共通ファイルは14件、新規は `wsl-dotfiles` スキルと `.gitignore` と symlink 2件）。

## 3. 気づいたこと・知見 (Insights & Lessons Learned)

- 上流の正本は `.agent/`（単数形）で、`.claude` と `CLAUDE.md` は symlink である。`.agents/` は存在しないため、指定名のまま複製すると二重管理になる。取り込み時は「実体と symlink の別」を先に確認する必要がある。
- 指定範囲だけを取り込むと、上流文書の `docs/`・`Makefile` 前提が宙に浮く。本リポジトリでは各所を書き換え切らず、「§6.7 の配置への読み替え」を正として入口文書だけを整合させた。上流スキル本文中の例示リンク切れ（5ファイル25件）は上流でも同一の既存事象であり、今回の作業では対象外とした。
- 同一ファイルへの編集を並行して発行すると、後勝ちで一部が失われることがある（実際に発生し、監査で検出して順次に直した）。同一ファイルの複数編集は1件ずつ適用し、適用後に grep 等で実在確認をする。
- AI 作業環境の `/tmp` はターン間で消えることがある。再取得時は承認した調査時点の commit に固定すると、承認内容と実装のずれを防げる。

## 4. 次にすべきこと (Next Actions)

- ユーザーレビューと PR のマージ判断（本ブランチから `main` 向け PR を作成予定。マージはユーザー判断）。
- dotfiles 設計の再開: `wsl-dotfiles` スキルの「設計を再開するときの順序」に沿って、参照先と現行設定の比較から具体案を提示する。未決事項（`AGENTS.md §6.4`）はこのタスクでは決定していない。
- スキルの削減は行っていない（全保持が承認内容）。棚卸しが必要になったら候補一覧の承認を経てから削除する。
- `README.md` は今回の合意で変更していない。プロジェクト概要の整備は別タスクとする。
