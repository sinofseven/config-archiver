# プログラムの名前を変える
## 要望

名前を `config-archiver` に変えて欲しい。

## プラン

1. `Cargo.toml` の `name` フィールドを `config-backup-archiver` → `config-archiver` に変更
2. `cargo clean` で旧名のビルドアーティファクトを削除
3. `cargo build` で `Cargo.lock` を再生成し、ビルド確認
4. `cargo test` でテスト通過を確認

## 完了サマリー

- 完了日時: 2026-04-14T21:41:28+09:00
- `Cargo.toml` の `name` フィールドを `config-backup-archiver` → `config-archiver` に変更
- `cargo clean` → `cargo build` → `cargo test` すべて成功
- バイナリ名が `config-archiver` になったことを確認（`config_archiver-9b22dd9da207b939`）