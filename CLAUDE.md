# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 概要
- `~/.config/`の内容をバックアップするためのCLIツール
- globで指定したファイルのみバックアップする
- バックアップしたファイルはtarアーカイブにまとめ、zstdで圧縮する

## 野望
- バックアップのS3へのアップロード機能を持たせたい
- globで指定していないファイルの一覧を生成する機能も欲しい
- Linuxの `systemd` やmacの `launchctl` のスクリプトを生成する機能も欲しい

## 開発コマンド

- ビルド: `cargo build`
- テスト全実行: `cargo test`
- 単一テスト実行: `cargo test <テスト名>`
- Lint: `cargo clippy`
- フォーマット: `cargo fmt`
- フォーマットチェック: `cargo fmt -- --check`

## Kanban ワークフロー

タスク管理に kanban 方式を採用している。詳細は `.claude/kanban-workflow.md` を参照。

- `kanban/` にタスクファイル（`{xxxx}_{title}.md`）を配置する
- `logs/` に同名のログファイルが自動生成される（git 管理対象）
- **タスク開始時は `/kanban` コマンドを使用すること**
- `/kanban` はまずプランモードで計画を立て、承認後に実装に移る
- **タスク作業中は、各ステップ完了時に必ずログファイルを更新すること**
- kanban ファイルへの追記時・ログへの記録時は JST タイムゾーンの ISO 8601 形式で日時を記載する
