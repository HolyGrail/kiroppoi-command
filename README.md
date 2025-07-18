# kiroppoi-command

Kiroっぽい開発フローをClaude Codeで実現するカスタムコマンド集です。

要件定義から実装、検証まで一貫した開発フローを提供し、進捗管理とドキュメント化を自動化します。

## 特徴

- **構造化された開発フロー**: 要件定義 → 設計 → 実装 → 検証の流れを体系化
- **シンプルなファイル構造**: 3つのファイル（要件・設計・タスク）で完結
- **柔軟な進捗管理**: タスクの依存関係と完了状態を管理
- **低い学習コスト**: 6つの直感的なコマンドのみ

## インストール

このリポジトリをクローンして、プロジェクトのルートディレクトリに配置します：

```bash
# プロジェクトのルートディレクトリで実行
git clone https://github.com/HolyGrail/kiroppoi-command.git .claude-kiroppoi
ln -s .claude-kiroppoi/.claude .claude
```

または、`.claude/commands/`ディレクトリに直接コピー：

```bash
cp -r kiroppoi-command/.claude/commands/* your-project/.claude/commands/
```

## 使い方

### 基本的な開発フロー

```bash
# 1. 新しい機能を開始
/kiroppoi-spec user-authentication

# 2. 要件を定義
/kiroppoi-requirements メールとパスワードでログイン、JWT認証、パスワードリセット機能

# 3. 設計を作成
/kiroppoi-design

# 4. タスクを実装（繰り返し）
/kiroppoi-implement
/kiroppoi-implement
/kiroppoi-implement

# 5. 検証
/kiroppoi-validate
```

### 統合ワークフロー

すべてのステップを対話的に実行：

```bash
/kiroppoi-flow ユーザー認証機能を作りたい
```

## コマンド一覧

### /kiroppoi-spec [feature-name]
スペック（機能仕様）の初期化と切り替えを行います。

- 引数なし: 現在のスペックと一覧を表示
- 新規機能名: 新しいスペックを作成
- 既存機能名: スペックを切り替え

### /kiroppoi-requirements [description]
現在のスペックの要件定義を作成します。ユーザーストーリー、機能要件、非機能要件を構造化して記録。

### /kiroppoi-design
要件定義を基に技術設計を作成し、実装タスクを自動生成します。

### /kiroppoi-implement
次の実装タスクを実行します。設計書を参照しながらコードを生成し、進捗を更新。

### /kiroppoi-validate
実装の検証を行い、要件との整合性やコード品質をチェックします。

### /kiroppoi-flow [description]
要件定義から実装まで、すべてのステップを対話的に実行します。

## ファイル構造

```
.claude/
├── current-spec.txt              # 現在作業中のスペック名
└── spec/
    └── {feature-name}/
        ├── requirements.md       # 要件定義書
        ├── design.md            # 技術設計書
        └── tasks.md             # タスクリストと進捗
```

## 実装例

### ユーザー認証機能の実装

```bash
# スペックを作成
/kiroppoi-spec user-auth

# 要件を定義
/kiroppoi-requirements "
- メールアドレスとパスワードでログイン
- JWT トークンで認証管理
- 24時間でトークン有効期限
- パスワードリセット機能
"

# 設計を生成（タスクも自動作成される）
/kiroppoi-design

# タスクを順次実装
/kiroppoi-implement  # → User モデルの作成
/kiroppoi-implement  # → ログインAPIの実装
/kiroppoi-implement  # → JWT管理の実装

# 実装を検証
/kiroppoi-validate
```

## タスク管理

`tasks.md`ファイルで以下を管理：

- **未完了タスク**: 実装待ちのタスク一覧
- **完了タスク**: 実装済みタスクと詳細情報
- **依存関係**: タスク間の依存を明示
- **メモ**: 実装時の決定事項や検証結果

## ベストプラクティス

1. **要件は具体的に**: 曖昧な要件は後で問題になります
2. **タスクは小さく**: 1-2時間で完了できる粒度に分割
3. **こまめに検証**: 各タスク完了後に`/kiroppoi-validate`
4. **ドキュメント更新**: 実装中の決定事項は`tasks.md`に記録

## 開発フロー図

```
[要件定義] → [技術設計] → [タスク生成]
                              ↓
[検証] ← [実装] ← [実装] ← [実装]
  ↓
[完了]
```

## トラブルシューティング

### スペックが見つからない
```bash
# 現在のスペックを確認
/kiroppoi-spec

# 新しくスペックを作成
/kiroppoi-spec my-feature
```

### タスクの依存関係でブロック
依存タスクを先に完了させるか、`tasks.md`を直接編集して依存関係を調整。

### 検証でエラーが多い
小さな修正は`tasks.md`に追加タスクとして記録し、`/kiroppoi-implement`で対応。