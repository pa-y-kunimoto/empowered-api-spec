# クイックスタートガイド

empowered-api-specを使って、5分でAPI仕様書を生成する方法を説明します。

## 前提条件

- AIエージェントへのアクセス（ChatGPT、Claude、GitHub Copilotのいずれか）
- 生成したいAPIの基本情報

## ステップバイステップ

### ステップ1: テンプレートを選ぶ（30秒）

用途に応じてテンプレートを選択：

| やりたいこと | 使うテンプレート |
|------------|----------------|
| 基本的なAPI仕様書を作りたい | `prompts/templates/basic-api-spec.md` |
| OpenAPI形式の仕様書を作りたい | `prompts/templates/openapi-spec.md` |
| 特定のエンドポイントの詳細を書きたい | `prompts/templates/endpoint-detail.md` |
| エラー処理を定義したい | `prompts/templates/error-handling.md` |

**初めての方は `basic-api-spec.md` から始めることをおすすめします。**

### ステップ2: テンプレートをコピー（30秒）

```bash
# GitHubからテンプレートを表示してコピー
# または、リポジトリをクローンして使用
git clone https://github.com/pa-y-kunimoto/empowered-api-spec.git
cd empowered-api-spec
```

ブラウザで直接見る場合：
1. [prompts/templates/](prompts/templates/) を開く
2. 使いたいテンプレートをクリック
3. 「Raw」ボタンをクリックして全文をコピー

### ステップ3: 情報を記入（2分）

テキストエディタにテンプレートを貼り付けて、`[...]` の部分を実際の情報に置き換えます。

**例：ユーザー管理APIの場合**

変更前：
```markdown
- **API名**: [APIの名前を記入]
- **バージョン**: [バージョン番号を記入]
```

変更後：
```markdown
- **API名**: User Management API
- **バージョン**: v1.0.0
```

### ステップ4: AIエージェントに入力（1分）

カスタマイズしたプロンプトをAIエージェントに貼り付けます。

#### ChatGPT/Claudeの場合：
1. ブラウザでChatGPT/Claudeを開く
2. プロンプト全体をコピー＆ペースト
3. 送信ボタンをクリック

#### GitHub Copilot Chatの場合：
1. VSCodeを開く
2. Copilot Chatパネルを開く（Cmd/Ctrl + Shift + I）
3. プロンプト全体を入力
4. Enter

### ステップ5: 結果を確認・保存（1分）

生成されたAPI仕様書を確認して、必要に応じて修正を依頼します。

```markdown
# 例：追加で依頼する場合
「エラーレスポンスの例をもっと詳しく追加してください」
「curlコマンドの例を追加してください」
```

満足したら、生成された仕様書を保存：
```bash
# Markdownファイルとして保存
cp api-specification.md docs/
```

## 完全な例

### 入力するプロンプト例

```markdown
# 基本的なAPI仕様書生成プロンプト

以下の情報に基づいて、詳細なAPI仕様書を生成してください。

## API概要
- **API名**: Todo Management API
- **バージョン**: v1.0.0
- **ベースURL**: https://api.example.com/v1
- **認証方式**: Bearer Token

## エンドポイント一覧

### エンドポイント1
- **メソッド**: GET
- **パス**: /todos
- **説明**: Todo一覧を取得
- **リクエストパラメータ**: status (completed/pending), page, limit
- **レスポンス**: Todoオブジェクトの配列

### エンドポイント2
- **メソッド**: POST
- **パス**: /todos
- **説明**: 新しいTodoを作成
- **リクエストパラメータ**: なし
- **レスポンス**: 作成されたTodoオブジェクト

[以下、テンプレートの残りの部分...]
```

### 期待される出力

AIが以下のような詳細な仕様書を生成します：

```markdown
# Todo Management API 仕様書

## 1. 概要

Todo Management APIは、タスク管理機能を提供するRESTful APIです...

## 2. 認証

本APIはBearer Token認証を使用します...

Authorization: Bearer YOUR_TOKEN_HERE

## 3. エンドポイント詳細

### 3.1 GET /todos - Todo一覧取得

#### リクエスト
- Method: GET
- URL: https://api.example.com/v1/todos
- Headers:
  - Authorization: Bearer {token}
  - Content-Type: application/json

#### クエリパラメータ
| パラメータ | 型 | 必須 | デフォルト | 説明 |
|-----------|-----|------|-----------|------|
| status | string | No | all | フィルタ条件 |
| page | integer | No | 1 | ページ番号 |
| limit | integer | No | 20 | 件数 |

[以下続く...]
```

## 次のステップ

- より詳細な仕様が必要な場合は `endpoint-detail.md` を使用
- OpenAPI形式が必要な場合は `openapi-spec.md` を使用
- エラー処理を詳しく定義したい場合は `error-handling.md` を使用

## よくある質問

### Q: プロンプトが長すぎる場合は？

A: 複数のエンドポイントがある場合は、以下のいずれかを試してください：
1. 基本情報だけ先に生成し、後からエンドポイントを追加
2. エンドポイントごとに `endpoint-detail.md` を使用
3. エンドポイントをグループ分けして複数回に分けて生成

### Q: AIの出力が思ったものと違う場合は？

A: 追加で指示を出して調整できます：
- 「もっと詳しく説明してください」
- 「コード例を追加してください」
- 「エラーケースを追加してください」

### Q: 生成された仕様書はそのまま使える？

A: 基本的には使えますが、以下を確認することをおすすめします：
- 技術的な正確性
- プロジェクト固有の要件との整合性
- セキュリティ上の考慮事項

### Q: チームで共有したい場合は？

A: 以下の方法があります：
1. 生成した仕様書をGitリポジトリにコミット
2. Swagger UIなどのツールでホスト
3. ドキュメントサイト（Docusaurus、MkDocsなど）に統合

## サポート

問題が発生した場合や質問がある場合は：
- [Issue](https://github.com/pa-y-kunimoto/empowered-api-spec/issues)を作成
- [詳細な使い方ガイド](docs/usage-guide.md)を参照

## 参考リンク

- [README](README.md) - プロジェクト概要
- [使い方ガイド](docs/usage-guide.md) - 詳細なガイド
- [コントリビューションガイド](CONTRIBUTING.md) - 貢献方法
- [プロンプト集](prompts/README.md) - すべてのテンプレート一覧
