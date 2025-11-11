# プロンプト集

このディレクトリには、**GitHub Copilot**や他のAIエージェントを使用してOpenAPI仕様書を拡充し、より詳細で実用的なAPI仕様書を生成するためのプロンプトテンプレートが含まれています。

## ディレクトリ構造

```
prompts/
├── templates/          # 再利用可能なプロンプトテンプレート
│   ├── copilot-openapi-enrichment.md   # GitHub Copilot用（推奨）
│   ├── openapi-enrichment.md           # 汎用OpenAPI拡充
│   ├── basic-api-spec.md               # 基本的なAPI仕様書生成
│   ├── openapi-spec.md                 # OpenAPI仕様書生成
│   ├── endpoint-detail.md              # エンドポイント詳細
│   └── error-handling.md               # エラーハンドリング
├── examples/           # 実際の使用例
│   ├── ecommerce-openapi-enrichment.md
│   └── user-management-api.md
└── README.md          # このファイル
```

## テンプレート一覧

### 🌟 GitHub Copilot用テンプレート（推奨）

#### copilot-openapi-enrichment.md
**GitHub Copilot Chatで使用するための最適化されたテンプレート**

**用途**: GitHub Copilot Chatを使って、既存のOpenAPI仕様書を対話的に拡充

**特徴**:
- 簡潔なプロンプト例
- 段階的な拡充方法
- 対話形式での使い方
- トラブルシューティング
- Copilot Chat特有の使い方

**使用方法**:
1. VSCodeでCopilot Chat を開く（`Ctrl+Shift+I` または `Cmd+Shift+I`）
2. 簡易プロンプトをコピーしてOpenAPI仕様書と一緒に入力
3. Copilotと対話しながら段階的に拡充

**最も簡単な使い方**:
```
このOpenAPI仕様書をユースケース中心に拡充してください

[OpenAPI仕様書をここに貼り付け]
```

**適している場合**:
- VSCodeを使用している
- 対話的に仕様書を作成したい
- 段階的に詳細化したい
- GitHub Copilotのサブスクリプションがある

**対象者**: すべての人（**最も推奨**）

---

### 📚 汎用テンプレート

#### openapi-enrichment.md
**ChatGPT、Claude等でも使える詳細なテンプレート**

**用途**: 既存のOpenAPI仕様書（YAML/JSON）を入力として、ユースケース中心の詳細な仕様書を生成

**特徴**:
- 完全な仕様定義
- すべての要求事項を含む
- ユースケースごとのAPI呼び出し手順を自動生成
- 専門用語の定義を追加
- API間の関連性を明確化
- ID指定APIの利用文脈を説明

**適している場合**:
- ChatGPTやClaudeを使用する
- 一度に完全な仕様書を生成したい
- 既にOpenAPI仕様書がある

**対象者**: OpenAPI仕様書を持っている人（汎用AIエージェント用）

---

### 📝 補助テンプレート

以下のテンプレートは、OpenAPI仕様書がない場合や、特定の用途に使用します。

#### 1. basic-api-spec.md
基本的なAPI仕様書を生成するためのテンプレート。
RESTful APIの概要、エンドポイント、認証方式などを含む標準的な仕様書を生成します。

**対象者**: OpenAPI仕様書がなく、ゼロから仕様書を作成したい人

#### 2. openapi-spec.md
OpenAPI 3.0形式の仕様書（YAML）を生成するためのテンプレート。
Swagger UIなどのツールで使用できる標準形式の仕様書を生成します。

**対象者**: OpenAPI仕様書自体を作成したい人

#### 3. endpoint-detail.md
特定のエンドポイントについて詳細な仕様書を生成するためのテンプレート。
リクエスト、レスポンス、エラー処理、使用例などを網羅的に記載します。

**対象者**: 特定のエンドポイントだけを詳しく説明したい人

#### 4. error-handling.md
API全体のエラーハンドリング戦略を定義するためのテンプレート。
エラーコード、エラーメッセージ形式、ベストプラクティスなどを定義します。

**対象者**: エラー処理を標準化したい人

## 使い方

### 基本的な流れ（GitHub Copilot - 推奨）

1. **VSCodeでCopilot Chatを開く**: `Ctrl+Shift+I` または `Cmd+Shift+I`
2. **簡易プロンプトを使用**: 
   ```
   このOpenAPI仕様書をユースケース中心に拡充してください
   [あなたのOpenAPI仕様書]
   ```
3. **対話的に拡充**: 必要に応じて追加の質問や修正を依頼
4. **結果を確認**: 生成された仕様書を確認・保存

詳細は `copilot-openapi-enrichment.md` を参照。

### 基本的な流れ（ChatGPT/Claude等）

1. **OpenAPI仕様書を用意**: 既存のOpenAPI 3.0仕様書（YAML/JSON）を準備
2. **テンプレートを使用**: `openapi-enrichment.md` を開く
3. **仕様書を埋め込む**: 指定箇所にOpenAPI仕様書の内容を貼り付け
4. **AI入力**: 完成したプロンプトをChatGPT/Claudeに入力
5. **拡充された仕様書を取得**: AIが詳細な仕様書を生成

### OpenAPI仕様書がない場合

1. `basic-api-spec.md` または `openapi-spec.md` を使用
2. テンプレートの `[...]` 部分を実際の情報で置き換え
3. AIエージェントに入力して仕様書を生成

## 例（examples/）

`examples/` ディレクトリには、テンプレートを実際に使用した例が含まれています。

### ecommerce-openapi-enrichment.md
E-Commerce APIのOpenAPI仕様書を拡充する完全な例。
商品閲覧から購入までの一連のフローを含むRESTful APIの例です。

### user-management-api.md
ユーザー管理APIの仕様書を生成する完全な例。
基本的なCRUD操作を含むRESTful APIのプロンプト例です。

## GitHub Copilotでの使用パターン

### パターン1: 全体的な拡充
```
User: このOpenAPI仕様書をユースケース中心に拡充してください
[OpenAPI仕様書]

Copilot: [詳細な仕様書を生成]
```

### パターン2: 特定のユースケース
```
User: 「商品購入」のユースケースについて、API呼び出し手順を説明してください
[OpenAPI仕様書]

Copilot: [ユースケースの詳細手順を生成]
```

### パターン3: 段階的な拡充
```
User: まず全体概要を生成してください
[OpenAPI仕様書]

User: 次に GET /items について詳しく説明してください

User: 用語定義を追加してください
```

## カスタマイズのヒント

### OpenAPI仕様書拡充の場合

1. **完全なOpenAPI仕様書を用意**
   - `paths`、`components`、`schemas` を含む完全な仕様書が望ましい
   - 不完全な仕様書でも動作しますが、生成される説明の質が低下する可能性があります

2. **業務ドメイン情報を追加**
   - OpenAPI仕様書に加えて、業務的な文脈や用語の説明を追加すると、より適切な説明が生成されます
   
   例（Copilot Chat）:
   ```
   このAPIは、ECサイトの商品管理システムです。
   「SKU」は在庫管理単位を意味し、色・サイズごとに異なります。
   
   [OpenAPI仕様書]
   ```

3. **段階的なアプローチ（Copilot推奨）**
   - 最初に全体概要を生成
   - 次に特定のエンドポイントを詳細化
   - 最後に用語定義や関連性を追加

### ゼロから作成する場合

1. **具体的な情報を含める**
   - AIエージェントは具体的な情報があるほど良い仕様書を生成します
   - ❌ 悪い例: `API名: [API名]`
   - ✅ 良い例: `API名: E-Commerce Product API v2.0`

2. **データ例を提供する**
   - リクエスト/レスポンスの具体例を含めると、より実用的な仕様書になります

## 推奨される使用順序

### GitHub Copilot使用時（推奨）
1. ✅ VSCodeでCopilot Chatを開く
2. ✅ 簡易プロンプト + OpenAPI仕様書を入力
3. ✅ 対話的に拡充（必要に応じて追加質問）
4. ✅ 結果を確認・保存

### ChatGPT/Claude使用時
1. ✅ `openapi-enrichment.md` でOpenAPI仕様書を拡充
2. 必要に応じて `endpoint-detail.md` で個別詳細化
3. 必要に応じて `error-handling.md` でエラー処理統一

### OpenAPI仕様書がない場合
1. `openapi-spec.md` でOpenAPI仕様書を作成
2. 上記のいずれかの方法で拡充
3. または `basic-api-spec.md` で直接仕様書を作成

## 貢献

新しいテンプレートや改善案がある場合は、Pull Requestを作成してください。

### 新しいテンプレートを追加する場合

1. `prompts/templates/` に `.md` ファイルを作成
2. 明確な構造とプレースホルダーを使用
3. このREADMEに説明を追加
4. `examples/` に使用例を追加

## 参考資料

詳細な使い方については、以下のドキュメントを参照してください：

- [メインREADME](../README.md) - リポジトリ全体の概要とGitHub Copilotでの使い方
- [GitHub Copilot Instructions](../.github/copilot-instructions.md) - Copilot用の詳細な指示
- [使い方ガイド](../docs/usage-guide.md) - 詳細な使用方法とベストプラクティス
