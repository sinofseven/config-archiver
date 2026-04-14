# ログ: プログラムの名前を変える

- 開始日時: 2026-04-14T21:41:03+09:00
- 完了日時: 2026-04-14T21:41:28+09:00

## タスク概要

名前を `config-archiver` に変えて欲しい。

## 調査結果

- `Cargo.toml` の `name = "config-backup-archiver"` が唯一の手動変更対象
- `Cargo.lock` は cargo build で自動再生成される
- `src/main.rs` は `fn main() { println!("Hello, world!"); }` のみで参照なし
- その他のファイル（CLAUDE.md, AGENTS.md, .claude/*, kanban/*, logs/*）に旧名の参照なし
- `target/` 配下のアーティファクトは cargo clean → cargo build で自動更新される

## 実装プラン

1. `Cargo.toml` の `name` フィールドを `config-backup-archiver` → `config-archiver` に変更
2. `cargo clean` で旧名のビルドアーティファクトを削除
3. `cargo build` で `Cargo.lock` を再生成し、ビルド確認
4. `cargo test` でテスト通過を確認

## プランニング経緯

初回提案がそのまま承認された。

## 編集したファイル

- `Cargo.toml`: `name` フィールドを変更

## 実行したコマンド

- `cargo clean`
- `cargo build`
- `cargo test`

## 判断・意思決定

- ディレクトリ名（`config-backup-archiver/`）はリネームしない: git 管理上の複雑さを避けるためスコープ外とした

## エラー・問題

なし

---

完了日時: 2026-04-14T21:41:28+09:00
