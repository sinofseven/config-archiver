# 0000_sync_agents_md 作業ログ

## 基本情報

- **タスクファイル**: kanban/0000_sync_agents_md.md
- **開始日時**: 2026-04-14T15:39:28+09:00
- **完了日時**: 2026-04-14T15:40:55+09:00

## タスク概要

GithubのPRレビューにCodexを使用するつもりです。
ですがCodexはCLAUDE.mdを読み込まないので、CLAUDE.mdからAGENTS.mdを作成し、CLAUDE.mdに変更があれば自動でAGENTS.mdが追従するようにしたい。

レビューにしか使わないのでkanbanワークフローについてはAGENTS.mdに書かなくて良い。

## 調査結果

### 調べたファイル

- `CLAUDE.md`: プロジェクト案内。セクション: 概要、野望、開発コマンド、Kanbanワークフロー
- `.github/workflows/codex-code-review.yml`: Codex PRレビューワークフロー（既存）
- `.github/codex/codex-prompt.md`: Codexへのレビュー指示（既存）
- `.claude/settings.json`: Claude Code hook設定
- `.claude/hooks/check-kanban.sh`: 既存hookスクリプト例
- `AGENTS.md`: 未存在（新規作成対象）

### 現状の構造

- `.claude/settings.json` に `UserPromptSubmit` hookが定義されている
- hookスクリプトは `.claude/hooks/` に格納されている
- `PostToolUse` hookを追加することでファイル編集後の自動実行が可能
- ユーザーは "Claude Code hook" 方式と "ヘッダー・文言の調整" を選択

### CLAUDE.md の変換内容

1. `# CLAUDE.md` → `# AGENTS.md`
2. `This file provides guidance to Claude Code (claude.ai/code)` → `This file provides guidance to AI coding agents`
3. `## Kanban ワークフロー` セクション以降を除去

## 実装プラン

1. `.claude/hooks/sync-agents-md.sh` を新規作成（変換スクリプト）
2. `.claude/settings.json` に `PostToolUse` hook を追加
3. スクリプトを手動実行して `AGENTS.md` を初回生成

## 編集したファイル

| ファイル | 変更内容 |
|---------|---------|
| `.claude/hooks/sync-agents-md.sh` | 新規作成 |
| `.claude/settings.json` | PostToolUse hook 追加 |
| `AGENTS.md` | 新規生成 |

## 実行したコマンド

```bash
bash .claude/hooks/sync-agents-md.sh
```

## 判断・意思決定

- `PostToolUse` の matcher は `(Edit|Write)` として Edit/Write 両ツールをカバー
- スクリプトは差分チェックを行い、変更がない場合は何もしない（冪等）
- `## Kanban ワークフロー` 以降を全除去（最後のセクションのため）

## エラー・問題

- 特になし
