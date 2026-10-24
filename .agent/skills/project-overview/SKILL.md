---
name: project-overview
description: wsl-home（WSL Ubuntu向けdotfilesリポジトリ）の全体像（目的・現在地・構成・前提）を掴む。新規セッションの最初、または全体把握が必要なときに読む。規約は AGENTS.md §6、進捗は docs/task-list.md、WSL環境とdotfiles設計の前提知識は wsl-dotfiles スキルを参照。Use when starting a new session or needing overall context for wsl-home.
---

# Project Overview — wsl-home

> 本リポジトリは、Windows 11 + WSL Ubuntu の開発環境のための **dotfiles リポジトリ**です。
> 現在は **設計段階** で、配置対象の設定ファイルと自前ツール本体はまだ入っていません。
> 2026-10-19 に `shiratama644/TEMPLATE_REPO`（commit `267d9d0`）から土台一式を取り込み、本プロジェクト用に調整しました。

## 目的

- ローカル（WSL）での編集と、リモートからの Git 更新の両方が同じ設定に反映される dotfiles の仕組みを作ること（合意済みの方式は [`wsl-dotfiles`](../wsl-dotfiles/SKILL.md) を正とします）。
- 配置・検査は、chezmoi の設計を参考にした自前ツール（Bun + TypeScript）が担います。引っ越し（別端末への移行）・暗号化保存・CLI と TUI の二段構成までが機能要求です（[`docs/arch/product.md`](../../../docs/arch/product.md)）。
- zsh の構造と独自コマンド `gg` は、参照リポジトリ `shiratama644/UbuntuHome` の構造・操作感を参考にします（無条件にコピーするものではありません）。
- 既存の開発環境（mise / uv / Go / Rust / Git / Docker / Starship の見た目）を壊さずに、段階的に移行すること。

## 現在地

| 項目 | 状態 |
| :--- | :--- |
| 工程 | 土台整備中（進捗の正本は [`docs/task-list.md`](../../../docs/task-list.md)）。配置方式は決定済み、設計文書はこれから |
| リポジトリの中身 | `AGENTS.md` / `.agent/` / `docs/` / `Makefile` / `scripts/` / CI 等の土台一式。配置対象の設定とツール本体はまだ無い |
| ユーザー実環境への変更 | 未実施（インストール・ファイル移動・リンク作成は設計合意後） |
| 次の作業 | 自前ツールの設計文書の作成と承認（task-list の DESIGN-2） |

## リポジトリ構成

| パス | 役割 |
|---|---|
| `AGENTS.md` | Agent が必ず守る作業規約。§6 が本プロジェクト固有の正本（`CLAUDE.md` はその symlink） |
| `.agent/` | Agent 設定と知識（rules / skills / hooks / agents など。`.claude` はその symlink） |
| `docs/` | ドキュメント一式。進捗は `task-list.md`、仕様は `arch/`、計画は `planning/` |
| `Makefile` / `scripts/` | 検証の入口と補助スクリプト。検証手段の正本は `AGENTS.md §6.1` |
| `.gitignore` | 秘密情報・履歴・個人設定をコミットしないための除外設定 |
| `README.md` | プロジェクト概要 |

将来、配置対象の設定（`zsh/` 等）と自前ツールが追加される想定ですが、レイアウト詳細は未決です。勝手に確定仕様として作り込まないでください（`AGENTS.md §6.4`）。

## 環境の区別（最重要）

- **AI 作業環境**（サンドボックス内の clone）と **ユーザー実環境**（Windows 11 + WSL Ubuntu、`/home/ubuntu`）は別物です。AI 作業環境のコマンド結果を実環境の状態と混同しないでください。
- 実環境のバージョン・パス等の値は、2026-10-18〜19 日にユーザーから共有された時点のものです。使う前に現在値の再確認を前提としてください。詳細な前提知識は [`wsl-dotfiles`](../wsl-dotfiles/SKILL.md) にあります。

## ドキュメントと進捗

- 進捗の正本は [`docs/task-list.md`](../../../docs/task-list.md)。文書の目次は [`docs/README.md`](../../../docs/README.md)。
- 作業規約： `AGENTS.md`（§6 はプロジェクト固有）
- ルール： `.agent/rules/`（入口は `rules/index.md`）
- スキル： `.agent/skills/`（入口は `skills/index.md`。全て読まず、読み方ガイドで必要なものだけ読む）
- フック： `.agent/hooks/`（入口は `hooks/index.md`）
- 実行記録： `.agent/logs/` と `docs/audit/activity.md`（追加のみ）

## 関連

- WSL 環境・dotfiles 設計の前提知識： [`wsl-dotfiles`](../wsl-dotfiles/SKILL.md)
- 製品定義： [`docs/arch/product.md`](../../../docs/arch/product.md) / 構成： [`docs/arch/architecture.md`](../../../docs/arch/architecture.md)
- 上流： `shiratama644/TEMPLATE_REPO`（取り込み元。commit `267d9d0`、2026-10-19）
- 参照リポジトリ： `shiratama644/UbuntuHome`（zsh 構造と `gg` の参考。外部リポジトリであり、本リポジトリには取り込まない）
