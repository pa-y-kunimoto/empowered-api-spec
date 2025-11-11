# Empowered API Spec

**GitHub Copilot**を使用して、既存のOpenAPI仕様書を拡充し、より理解しやすく実用的なAPI仕様書を生成するためのリポジトリです。

## 概要

このリポジトリは、**既存のOpenAPI仕様書（YAML/JSON）を入力として**、**GitHub Copilot**や他のAIエージェントを使ってより詳細で包括的なAPI仕様書を生成するためのプロンプトテンプレートを提供します。

### 特徴

- 🤖 **GitHub Copilot最適化**: GitHub Copilot Chatで直接使用できるプロンプト
- 📖 **ユースケース中心**: 単なるリファレンスではなく、実際の利用シーンに基づいた説明
- 🔗 **API間の関連性**: どのAPIをどの順番で呼び出すかを明確化
- 📚 **用語定義**: 専門用語を丁寧に説明
- 🎯 **手順重視**: API利用者が迷わないよう、具体的な手順を提示

## クイックスタート（GitHub Copilot）

### GitHub Copilot Chatでの使用

1. **VSCodeでCopilot Chatを開く**
   - `Ctrl+Shift+I` (Windows/Linux) または `Cmd+Shift+I` (Mac)
   - または、サイドバーのCopilotアイコンをクリック

2. **プロンプトを入力**
   ```
   このOpenAPI仕様書をユースケース中心に拡充してください
   
   [あなたのOpenAPI仕様書をここに貼り付け]
   ```

3. **結果を確認**
   - Copilotが詳細な仕様書を生成
   - 必要に応じて追加の質問や修正依頼が可能

### 詳細なプロンプトテンプレート

より詳細な制御が必要な場合は、`prompts/templates/copilot-openapi-enrichment.md` を参照してください。

## ディレクトリ構造

```
empowered-api-spec/
├── .github/
│   └── copilot-instructions.md    # GitHub Copilot用の指示書
├── prompts/
│   ├── templates/
│   │   ├── copilot-openapi-enrichment.md  # GitHub Copilot用テンプレート（推奨）
│   │   └── openapi-enrichment.md          # 汎用テンプレート
│   └── examples/                   # 具体的な使用例
└── docs/                           # ドキュメント
```

## 使い方

### 方法1: GitHub Copilot Chat（推奨）

#### 基本的な使い方
```
User: このOpenAPI仕様書を拡充してください
[OpenAPI YAML/JSON]

Copilot: 承知しました。ユースケース中心の詳細な仕様書を生成します...
```

#### 特定のユースケースにフォーカス
```
User: 「商品購入」のユースケースについて、API呼び出し手順を教えてください
[OpenAPI YAML/JSON]
```

#### 段階的な拡充
```
User: まず全体概要を生成してください
[OpenAPI YAML/JSON]

User: 次に、GET /items エンドポイントについて詳しく説明してください

User: 各APIの用語定義を追加してください
```

### 方法2: 他のAIエージェント（ChatGPT、Claude）

1. `prompts/templates/openapi-enrichment.md` を開く
2. テンプレート内の指定箇所にOpenAPI仕様書を貼り付け
3. 完成したプロンプトをAIエージェントに入力

## プロンプトテンプレート

### 主要テンプレート（GitHub Copilot用）

- **copilot-openapi-enrichment.md**: GitHub Copilot Chat用に最適化されたテンプレート
  - 簡潔なプロンプト例
  - 対話形式での使い方
  - トラブルシューティング

### 汎用テンプレート

- **openapi-enrichment.md**: ChatGPT、Claude等でも使える詳細なテンプレート
  - 完全な仕様定義
  - すべての要求事項を含む

### 補助テンプレート

- **basic-api-spec.md**: OpenAPI仕様がない場合の基本仕様書生成
- **endpoint-detail.md**: 特定のエンドポイントの詳細説明
- **error-handling.md**: エラー処理の標準化

## 生成される仕様書の構成

Copilotが生成する仕様書には以下が含まれます：

### 1. API全体概要
- システムの目的
- 想定ユースケース一覧
- 各ユースケースのAPI呼び出し手順（順序付き）

### 2. API詳細仕様（各APIについて）
- **概要**: APIが果たす目的
- **用語定義**: 専門用語の説明
- **リクエスト仕様**: メソッド、パラメータ、ボディ
- **レスポンス仕様**: 成功/エラーレスポンス例
- **関連API・利用手順**: 前後に呼び出すAPI、IDの取得元

## 使用例

詳細な使用例は `prompts/examples/` ディレクトリを参照してください：

- `ecommerce-openapi-enrichment.md`: E-Commerce APIの完全な例

## GitHub Copilot Instructions

GitHub Copilotは `.github/copilot-instructions.md` の指示に従ってこのリポジトリを活用します。
Copilotは自動的にこのファイルを参照し、適切なテンプレートを使用して仕様書を拡充します。

## コントリビューション

新しいプロンプトテンプレートや改善案がある場合は、Pull Requestを作成してください。

## ライセンス

このプロジェクトはMITライセンスの下で公開されています。
