---
name: project-overview
description: wsl-home（WSL Ubuntu向けdotfilesリポジトリ）の全体像（目的・現在地・構成・前提）を掴む。新規セッションの最初、または全体把握が必要なときに読む。規約は AGENTS.md §6、WSL環境とdotfiles設計の前提知識は wsl-dotfiles スキルを参照。Use when starting a new session or needing overall context for wsl-home.
---

# Project Overview — wsl-home

> 本リポジトリは、Windows 11 + WSL Ubuntu の開発環境のための **dotfiles リポジトリ**です。
> 現在は **設計段階** で、配置対象の設定ファイルはまだ入っていません。
> 2026-10-19 に `shiratama644/TEMPLATE_REPO`（commit `267d9d0`）から `AGENTS.md` と `.agent/` を取り込み、本プロジェクト用に調整しました（`docs/`・`Makefile` 等は取り込み範囲外）。

## 目的

- ローカル（WSL）での編集と、リモートからの Git 更新の両方が同じ設定に反映される dotfiles の仕組みを作ること（合意済みの方式は [`wsl-dotfiles`](../wsl-dotfiles/SKILL.md) を正とします）。
- zsh の構造と独自コマンド `gg` は、参照リポジトリ `shiratama644/UbuntuHome` の構造・操作感を参考にします（無条件にコピーするものではありません）。
- 既存の開発環境（mise / uv / Go / Rust / Git / Docker / Starship の見た目）を壊さずに、段階的に移行すること。

## 現在地

| 項目 | 状態 |
| :--- | :--- |
| 工程 | dotfiles の設計段階（方式の詳細は未確定。`AGENTS.md §6.4` の未決リスト参照） |
| リポジトリの中身 | `AGENTS.md` / `.agent/`（Agent 設定一式）/ `README.md`（最小限）。配置対象の設定はまだ無い |
| ユーザー実環境への変更 | 未実施（インストール・ファイル移動・リンク作成は設計合意後） |
| 次の作業 | dotfiles 設計の再開（参照先と現行設定の比較 → 配置とリンク対応 → `gg` の仕様確定） |

## リポジトリ構成

| パス | 役割 |
|---|---|
| `AGENTS.md` | Agent が必ず守る作業規約。§6 が本プロジェクト固有の正本（`CLAUDE.md` はその symlink） |
| `.agent/` | Agent 設定と知識（rules / skills / hooks / agents など。`.claude` はその symlink） |
| `.gitignore` | 秘密情報・履歴・個人設定をコミットしないための除外設定 |
| `README.md` | プロジェクト概要（現在は最小限） |

将来、配置対象の設定（`zsh/` 等）が追加される想定ですが、レイアウトは未決です。勝手に確定仕様として作り込まないでください（`AGENTS.md §6.4`）。

## 環境の区別（最重要）

- **AI 作業環境**（サンドボックス内の clone）と **ユーザー実環境**（Windows 11 + WSL Ubuntu、`/home/ubuntu`）は別物です。AI 作業環境のコマンド結果を実環境の状態と混同しないでください。
- 実環境のバージョン・パス等の値は、2026-10-18〜19 日にユーザーから共有された時点のものです。使う前に現在値の再確認を前提としてください。詳細な前提知識は [`wsl-dotfiles`](../wsl-dotfiles/SKILL.md) にあります。

## ドキュメントと進捗

- `docs/` は未導入です。進捗と経緯は `.agent/logs/`（実行記録、追加のみ）と Git の履歴で追います。
- 作業規約： `AGENTS.md`（§6 はプロジェクト固有）
- ルール： `.agent/rules/`（入口は `rules/index.md`）
- スキル： `.agent/skills/`（入口は `skills/index.md`。全て読まず、読み方ガイドで必要なものだけ読む）
- フック： `.agent/hooks/`（入口は `hooks/index.md`）

## 関連

- WSL 環境・dotfiles 設計の前提知識： [`wsl-dotfiles`](../wsl-dotfiles/SKILL.md)
- テンプレート由来の汎用初期設定スキル（他プロジェクト向け。本リポジトリの調整は実施済み）： [`project-init`](../project-init/SKILL.md)
- 上流： `shiratama644/TEMPLATE_REPO`（取り込み元。commit `267d9d0`、2026-10-19）
- 参照リポジトリ： `shiratama644/UbuntuHome`（zsh 構造と `gg` の参考。外部リポジトリであり、本リポジトリには取り込まない）
