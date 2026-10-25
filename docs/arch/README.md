# docs/arch — 仕様書

ここは **どう作業するか・どういう構成か** の正本です。進捗は `../task-list.md`、個別の計画は `../planning/`。

wsl-home は、WSL Ubuntu 向け dotfiles と、その配置・検査を行う自前ツール（Bun + TypeScript）のリポジトリです。目的と機能要求は [product.md](./product.md)、プロジェクト固有の規約は `../../AGENTS.md §6` を参照してください。

## 実装・変更時に守ること

1. **仕様と実物を一致させる**。構成を変えたら、本ディレクトリと `../README.md`・`../../AGENTS.md` を同じ変更で更新する。
2. **ADR に反する変更をしない**。覆す場合は `../adr/` に新しい ADR を追加してから変える。
3. **分野固有の内容を共通部分に混ぜない**。特定の言語・ツール・分野の手順は、`AGENTS.md §6` またはプロジェクト側の文書に書く。
4. **ファイル名は短く正確に**。ハイフンは最大 1 つ。

## 読み方

| 状況 | 最初に読むもの |
|---|---|
| プロジェクトの目的を知りたい | [product.md](./product.md) |
| 自前ツール（dotctl）の設計を知りたい | [tool.md](./tool.md) |
| 構成と読み込みの流れを知りたい | [architecture.md](./architecture.md) |
| WSL・dotfiles の前提知識が要る | [`../../.agent/skills/wsl-dotfiles/SKILL.md`](../../.agent/skills/wsl-dotfiles/SKILL.md) |
| なぜそうなっているか知りたい | [`../adr/`](../adr/README.md) |
| 今どの段階か知りたい | [milestones.md](./milestones.md) → `../task-list.md` |

## 仕様書一覧

| ファイル | 内容 |
|---|---|
| [product.md](./product.md) | プロジェクトの目的・対象・機能要求・用語 |
| [tool.md](./tool.md) | 自前ツール dotctl の設計（仕様の正本、2026-10-25 承認済み） |
| [architecture.md](./architecture.md) | ディレクトリ構成・Agent の読み込みの流れ・責務の分担 |
| [milestones.md](./milestones.md) | 段階ごとの完了条件 |
