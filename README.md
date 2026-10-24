# wsl-home

Windows 11 + WSL Ubuntu の開発環境のための **dotfiles リポジトリ**です。
設定ファイルそのものに加え、配置・検査を行う自前ツール（chezmoi の設計を参考に Bun + TypeScript で新規実装する方針）を、このリポジトリで設計・開発します。

現在は **設計段階** です。配置対象の設定ファイルとツール本体はまだ入っておらず、実環境への適用も行っていません。決定済みの方針と未決事項は [`AGENTS.md` §6](./AGENTS.md) が正本です。

## 構成

| パス | 役割 |
| :--- | :--- |
| [`AGENTS.md`](./AGENTS.md) | Agent が必ず守る作業規約。§6 が本プロジェクト固有の正本（`CLAUDE.md` はその symlink） |
| [`.agent/`](./.agent/README.md) | Agent の設定と知識（rules / skills / hooks など。`.claude` はその symlink） |
| [`docs/`](./docs/README.md) | ドキュメント一式。進捗の正本は [`docs/task-list.md`](./docs/task-list.md) |
| [`docs/arch/product.md`](./docs/arch/product.md) | 何を作るか（目的・機能要求・非目標） |
| [`docs/arch/architecture.md`](./docs/arch/architecture.md) | どう作るか（構成と責務分担） |
| [`Makefile`](./Makefile) | 検証の入口（`make check` / `make links` / `make setup`）。検証手段の正本は `AGENTS.md §6.1` |
| [`scripts/`](./scripts/check_doc_links.py) | 文書リンク検査などの補助スクリプト |

将来、配置対象の設定（`zsh/`・`config/`・`git/`・`etc/`）と自前ツールが追加される想定です。詳細なレイアウトとリンク対応表は設計文書で確定します。

## 前提（守ること）

- 実体は本リポジトリ側に 1 つ置き、ホームからは一方向のシンボリックリンクを張ります（合意済み）。
- 本リポジトリは公開のため、秘密鍵・トークン・履歴・個人情報は置きません。暗号化して保存する機能を用意する場合も、SSH 秘密鍵は対象外とし、端末ごとに作り直す運用とします。
- Starship の現在の見た目や既存ツール構成（mise / uv / Go / Rust / Git / Docker）は変更しません。

## 由来

作業規約・ドキュメント・検証の土台（`AGENTS.md` / `.agent/` / `docs/` / `Makefile` / CI 等）は [`shiratama644/TEMPLATE_REPO`](https://github.com/shiratama644/TEMPLATE_REPO)（commit `267d9d0`）から 2026-10-19 に取り込み、本プロジェクト用に調整しました。zsh の構造と独自コマンド `gg` は `shiratama644/UbuntuHome` を参考にします（外部参照であり、取り込みはしません）。

## ライセンス

[LICENSE](./LICENSE) を参照してください。
