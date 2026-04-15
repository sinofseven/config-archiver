# 0005_update_add_kanban_sh 作業ログ

## 基本情報

- **タスクファイル**: kanban/0005_update_add_kanban_sh.md
- **開始日時**: 2026-04-15T13:59:27+09:00
- **完了日時**: 2026-04-15T14:00:02+09:00

## タスク概要

add_kanban.sh でファイルの作成をしているが、テンプレート機能が欲しい。
テンプレートは1種類固定で良い。

テンプレート:
```md
# title
## 要望

## 目的

```

## 調査結果

### bin/add_kanban.sh（変更対象）

現在の実装（全30行）:

```bash
#!/bin/bash
set -euo pipefail

if [ $# -ne 1 ]; then
    echo "Usage: $(basename "$0") <title>" >&2
    exit 1
fi

title="$1"
kanban_dir="$(cd "$(dirname "$0")/.." && pwd)/kanban"

# 既存ファイルから最大番号を取得
max_num=-1
for f in "$kanban_dir"/[0-9][0-9][0-9][0-9]_*.md; do
    [ -e "$f" ] || continue
    num="${f##*/}"
    num="${num%%_*}"
    num=$((10#$num))
    if [ "$num" -gt "$max_num" ]; then
        max_num="$num"
    fi
done

next_num=$((max_num + 1))
padded=$(printf "%04d" "$next_num")
filename="${kanban_dir}/${padded}_${title}.md"

touch "$filename"
echo "Created: $filename"
```

28行目の `touch "$filename"` が空ファイルを作成している箇所。ここを heredoc によるテンプレート書き込みに置き換える。

### .claude/kanban-workflow.md

kanban ファイルの基本構造として以下が定義されている（29〜39行）:
- `## 目的` セクション（Why）が必須項目
- `## 要望` セクション（What/How）
- `/kanban` コマンド実行時に目的セクションの存在確認が行われる

### kanban/0005_update_add_kanban_sh.md（タスクファイル）

タスクで指定されているテンプレートは:
```md
# title
## 要望

## 目的

```

## 実装プラン

`bin/add_kanban.sh` の28行目 `touch "$filename"` を、heredoc によるテンプレート書き込みに置き換える。

```bash
# 変更前
touch "$filename"

# 変更後
cat > "$filename" <<EOF
# ${title}
## 要望

## 目的

EOF
```

- `${title}` は既にスクリプト内で定義済み（9行目 `title="$1"`）
- 変更は1ファイル1箇所のみ
- 代替案として printf を使う方法もあるが、heredoc の方が可読性が高く、マルチラインテキストに適している

## プランニング経緯

### 初回提案

`touch "$filename"` を heredoc によるテンプレート書き込みに置き換える1箇所変更。

### ユーザーフィードバック

初回提案がそのまま承認された。

### 最終プラン

（変更なし）

## 会話内容

### [13:59] ユーザー指示

`/kanban` コマンドを実行。未完了タスク `0005_update_add_kanban_sh.md` を自動選択。

### [13:59] Claude 対応

- kanban ファイル、kanban-workflow.md、add_kanban.sh を読み込み
- プランモードに入り実装計画を策定
- kanban ファイルの `## プラン` セクションに計画を記載
- ExitPlanMode でユーザー承認を待つ → 承認

## 編集したファイル

| ファイル | 変更内容 |
|---------|---------|
| `bin/add_kanban.sh` | `touch` をテンプレート書き込みに置き換え |

## 実行したコマンド

```bash
bash bin/add_kanban.sh test_template
cat kanban/0006_test_template.md
rm kanban/0006_test_template.md
```

## 判断・意思決定

- heredoc を採用（printf より可読性が高くマルチラインに適切）
- テンプレートの末尾に空行を1行追加（ファイル末尾改行の慣習に従う）

## エラー・問題

（なし）
