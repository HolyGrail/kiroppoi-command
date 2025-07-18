---
description: "スペックを初期化または切り替えます"
---

引数に応じて以下の処理を実行してください：

## 1. 引数なしの場合

現在のスペックと利用可能なスペック一覧を表示：

まず `.claude/current-spec.txt` を読み込んで現在のスペックを確認。
次に `.claude/spec/` ディレクトリ内の全サブディレクトリを取得。
各スペックのタスク進捗を `tasks.md` から計算。

表示例：
```
現在のスペック: user-authentication

利用可能なスペック:
- user-authentication (実装中: 1/3 タスク完了)
- payment-integration (設計完了)
- dashboard-ui (完了)
```

## 2. 新しい機能名が指定された場合

- 機能名を正規化（小文字、ハイフン区切り）
- `.claude/spec/{feature-name}/` ディレクトリを作成
- 3つの空ファイルを作成:
  - requirements.md
  - design.md
  - tasks.md
- `.claude/current-spec.txt` に機能名を書き込み

```
✅ スペック 'user-authentication' を初期化しました
📁 .claude/spec/user-authentication/
```

## 3. 既存の機能名が指定された場合

- `.claude/current-spec.txt` を更新
- タスクの進捗状況を表示

```
✅ スペック 'payment-integration' に切り替えました
📊 進捗: 0/5 タスク完了
```

## エラー処理

- `.claude/` ディレクトリが存在しない場合は作成
- current-spec.txt が存在しない場合は空ファイルとして扱う
- ファイル読み取りエラーは適切に処理

$ARGUMENTS