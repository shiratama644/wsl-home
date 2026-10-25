# docs/planning — 計画書

計画書は、`docs/task-list.md` の各タスクを **どの順で、どの範囲で、何をもって完了とするか** に分解する場所です。仕様そのものの正本は `../arch/`。

## まず読むもの

| 順 | 文書 | いつ読むか | 内容 |
|---:|---|---|---|
| 1 | `../task-list.md` | 常に最初 | 状態・依存・次に着手できるタスク |
| 2 | 対象タスクの計画書 | 作業に入る前 | 目的、変更範囲、禁止事項、完了条件、停止条件 |
| 3 | `../research/README.md` | 根拠となる調査が必要な時 | 調査の入口 |
| 4 | `../arch/README.md` | 仕様の確認が必要な時 | 仕様書一覧 |

## 計画書の作り方

1. `../task-list.md` に行を追加する（ID を採番。再利用しない）。
2. [`_TEMPLATE.md`](./_TEMPLATE.md) をコピーして計画書を作る。ファイル名は短く正確に、ハイフンは最大 1 つ。
3. 計画書の完了条件を満たしたら、`task-list.md` の状態と証拠を更新する。

## 計画書の一覧

| 文書 | 対応 ID | 状態 | 役割 |
|---|---|---|---|
| [`_TEMPLATE.md`](./_TEMPLATE.md) | — | 現用 | 製品実装など個別タスクの必須形式 |
| [`TOOL_PLAN.md`](./TOOL_PLAN.md) | TOOL-1〜TOOL-5, MIG-1 | 案（承認待ち） | dotctl の段階型実装計画 |
| `INIT_STATE.md` | — | 実行時に作成 | 初期設定の作業記憶（スロット状態・予算）。承認前に書いてよい唯一のファイル |
| `INIT_PLAN.md` | — | 実行時に作成 | 承認済みの初期設定計画。書式は [`project-init`](../../.agent/skills/project-init/SKILL.md)。テンプレート本体には置かない |

dotctl の実装計画（`TOOL_PLAN.md`）を作成しました（案、承認待ち。`docs/task-list.md` の DESIGN-2 参照）。仕様の正本は [`../arch/tool.md`](../arch/tool.md) です。
