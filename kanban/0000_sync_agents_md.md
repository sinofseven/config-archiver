# AGENTS.mdをCLAUDE.mdに同期させる
## 要望
GithubのPRレビューにCodexを使用するつもりです。
ですがCodexはCLAUDE.mdを読み込まないので、CLAUDE.mdからAGENTS.mdを作成し、CLAUDE.mdに変更があれば自動でAGENTS.mdが追従するようにしたい。

レビューにしか使わないのでkanbanワークフローについてはAGENTS.mdに書かなくて良い。

## プラン

- `CLAUDE.md` をCodex向けに変換して `AGENTS.md` を生成するスクリプトを作成
- Claude Code の `PostToolUse` hookで Edit/Write 後に自動同期
- 変換内容: ヘッダー・説明文のCodex向け調整 + Kanbanセクションの除去

---

## 完了サマリー

- **完了日時**: 2026-04-14T15:40:55+09:00
- **対応内容**:
  - `.claude/hooks/sync-agents-md.sh` を新規作成（CLAUDE.md → AGENTS.md 変換スクリプト）
  - `.claude/settings.json` に `PostToolUse` hook（matcher: `(Edit|Write)`）を追加
  - `AGENTS.md` を初回生成（Codex向け文言に変換済み、Kanbanセクション除外）
- **変更ファイル**:
  - `.claude/hooks/sync-agents-md.sh`
  - `.claude/settings.json`
  - `AGENTS.md`