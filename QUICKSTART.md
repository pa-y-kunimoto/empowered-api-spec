# クイックスタートガイド

empowered-api-specを使って、既存のOpenAPI仕様書を5分で拡充する方法を説明します。

## 前提条件

- AIエージェントへのアクセス（ChatGPT、Claude、GitHub Copilotのいずれか）
- 既存のOpenAPI仕様書（YAML/JSON形式）

## ステップバイステップ

### ステップ1: OpenAPI仕様書を用意（30秒）

既存のOpenAPI 3.0仕様書を準備します。

- Swagger Editorなどで作成済みのもの
- 既存のAPI開発プロジェクトから生成されたもの
- 手動で作成したもの

**OpenAPI仕様書がない場合は、[こちら](#openapi仕様書がない場合)を参照**

### ステップ2: メインテンプレートを開く（30秒）

`prompts/templates/openapi-enrichment.md` をブラウザで開きます。

ブラウザで直接見る場合：
1. [prompts/templates/openapi-enrichment.md](prompts/templates/openapi-enrichment.md) を開く
2. 「Raw」ボタンをクリックして全文をコピー

またはリポジトリをクローン：
```bash
git clone https://github.com/pa-y-kunimoto/empowered-api-spec.git
cd empowered-api-spec
```

### ステップ3: OpenAPI仕様書を埋め込む（1分）

テキストエディタにテンプレートを貼り付けて、指定箇所にOpenAPI仕様書を貼り付けます。

**変更箇所：**
```markdown
## 📦 入力データ

以下にOpenAPI仕様書をYAMLまたはJSON形式で埋め込んでください。

```yaml
# ここにあなたのOpenAPI仕様書を貼り付け
```

### ステップ4: AIエージェントに入力（1分）

完成したプロンプトをAIエージェントに貼り付けます。

#### ChatGPT/Claudeの場合：
1. ブラウザでChatGPT/Claudeを開く
2. プロンプト全体をコピー＆ペースト
3. 送信ボタンをクリック

#### GitHub Copilot Chatの場合：
1. VSCodeを開く
2. Copilot Chatパネルを開く（Cmd/Ctrl + Shift + I）
3. プロンプト全体を入力
4. Enter

### ステップ5: 結果を確認・保存（2分）

生成された拡充版API仕様書を確認します。

AIが以下を含む詳細な仕様書を生成します：
- ✅ API全体概要とユースケース
- ✅ 各ユースケースでのAPI呼び出し手順
- ✅ 専門用語の定義
- ✅ API間の関連性と利用文脈
- ✅ 実用的なリクエスト/レスポンス例

満足したら保存：
```bash
# Markdownファイルとして保存
cp enriched-api-spec.md docs/
```

## 完全な例

### 入力例

`prompts/examples/ecommerce-openapi-enrichment.md` を参照してください。
E-Commerce APIのOpenAPI仕様書を拡充する完全な例です。

### 期待される出力

AIが以下のような詳細な仕様書を生成します：

```markdown
# E-Commerce API 仕様書

## 1. API全体概要

### システムの目的
このAPIは、オンラインショッピングサイトのバックエンド機能を提供し、
商品閲覧から購入までの一連のフローをサポートします。

### 想定ユースケース

#### ユースケース1: 商品を閲覧する
1. 商品一覧取得API（GET /items）
   - カテゴリでフィルタリング可能
2. 商品詳細取得API（GET /items/{id}）
   - 一覧で取得したitem_idを使用

#### ユースケース2: 商品を購入する
1. ユーザー認証API（POST /auth/login）
   - アクセストークンを取得
2. 商品一覧取得API（GET /items）
3. カート追加API（POST /cart）
   - 認証トークンが必要
4. 購入確定API（POST /orders）
   - 認証トークンが必要

## 2. API詳細仕様

### ユーザー認証（POST /auth/login）

#### 概要
ユーザーのメールアドレスとパスワードで認証を行い、
以降のAPI呼び出しで使用するアクセストークンを取得します。

#### 用語定義
- **アクセストークン**: 認証済みユーザーのセッションを識別するトークン
  - カート追加や購入確定など、認証が必要なAPIで使用
  - 有効期限は24時間

#### リクエスト仕様
- メソッド: POST
- エンドポイント: /auth/login
- リクエストボディ:
```json
{
  "email": "user@example.com",
  "password": "secure_password"
}
```

#### レスポンス仕様
成功時（200）:
```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIs...",
  "user_id": "user_123"
}
```

#### 関連API・利用手順
- このAPIで取得した `access_token` を、以降の認証が必要なAPIのAuthorizationヘッダーに設定します
- `user_id` を使って GET /users/{id} でユーザー情報を取得できます
- カート追加（POST /cart）や購入確定（POST /orders）の前に必ず実行してください

[以下続く...]
```

## OpenAPI仕様書がない場合

OpenAPI仕様書がまだない場合は、以下の手順で作成できます：

### オプション1: OpenAPI仕様書を生成
1. `prompts/templates/openapi-spec.md` を使用
2. APIの基本情報とエンドポイント情報を記入
3. AIに入力してOpenAPI仕様書を生成
4. 生成されたOpenAPI仕様書を使って `openapi-enrichment.md` で拡充

### オプション2: 直接仕様書を生成
1. `prompts/templates/basic-api-spec.md` を使用
2. APIの基本情報を記入
3. AIに入力して詳細な仕様書を直接生成

## 次のステップ

- より詳細な説明が必要な特定のエンドポイントがある場合は `endpoint-detail.md` を使用
- エラー処理を詳しく定義したい場合は `error-handling.md` を使用
- 生成された仕様書をチームで共有してレビュー

## よくある質問

### Q: OpenAPI仕様書が不完全な場合は？

A: 不完全でも動作しますが、以下を含めることを推奨します：
- `paths`: エンドポイントの定義
- `components/schemas`: データモデルの定義
- 各エンドポイントの `summary` と `description`

### Q: AIの出力が思ったものと違う場合は？

A: 追加で指示を出して調整できます：
- 「もっと詳しくユースケースを説明してください」
- 「API呼び出しの順序をフローチャートで示してください」
- 「専門用語の定義をもっと追加してください」

### Q: 生成された仕様書はそのまま使える？

A: 基本的には使えますが、以下を確認することをおすすめします：
- 業務ドメイン固有の情報の正確性
- セキュリティ要件との整合性
- 実際のAPI実装との一致

### Q: 英語のOpenAPI仕様書でも使える？

A: はい、使えます。ただし、生成される仕様書は日本語になります。
英語の仕様書が必要な場合は、プロンプトに「英語で生成してください」と追加してください。

## サポート

問題が発生した場合や質問がある場合は：
- [Issue](https://github.com/pa-y-kunimoto/empowered-api-spec/issues)を作成
- [詳細な使い方ガイド](docs/usage-guide.md)を参照

## 参考リンク

- [README](README.md) - プロジェクト概要
- [使い方ガイド](docs/usage-guide.md) - 詳細なガイド
- [コントリビューションガイド](CONTRIBUTING.md) - 貢献方法
- [プロンプト集](prompts/README.md) - すべてのテンプレート一覧
