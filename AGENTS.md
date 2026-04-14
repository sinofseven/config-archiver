# AGENTS.md

This file provides guidance to AI coding agents when working with code in this repository.

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
