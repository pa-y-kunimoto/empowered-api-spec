# リポジトリ構造

このドキュメントは、empowered-api-specリポジトリの構造を視覚的に説明します。

## ディレクトリツリー

```
empowered-api-spec/
│
├── 📄 README.md                          # プロジェクト概要（最初に読む）
├── 📄 QUICKSTART.md                      # 5分で始めるガイド
├── 📄 CONTRIBUTING.md                    # 貢献方法
├── 📄 LICENSE                            # MITライセンス
├── 📄 .gitignore                         # Git除外設定
│
├── 📁 prompts/                           # プロンプト格納ディレクトリ
│   ├── 📄 README.md                      # プロンプト集の説明
│   │
│   ├── 📁 templates/                     # 再利用可能なテンプレート
│   │   ├── 📄 basic-api-spec.md          # 基本的なAPI仕様書生成
│   │   ├── 📄 openapi-spec.md            # OpenAPI 3.0仕様書生成
│   │   ├── 📄 endpoint-detail.md         # エンドポイント詳細仕様
│   │   └── 📄 error-handling.md          # エラーハンドリング仕様
│   │
│   └── 📁 examples/                      # 具体的な使用例
│       └── �� user-management-api.md     # ユーザー管理API例
│
└── 📁 docs/                              # ドキュメント
    └── 📄 usage-guide.md                 # 詳細な使い方ガイド
```

## ファイルの役割

### ルートディレクトリ

| ファイル | 用途 | 読むべきタイミング |
|---------|------|------------------|
| `README.md` | プロジェクト概要 | 最初に |
| `QUICKSTART.md` | クイックスタート | すぐに使い始めたい時 |
| `CONTRIBUTING.md` | 貢献ガイド | プロジェクトに貢献したい時 |
| `LICENSE` | ライセンス情報 | 利用条件を確認したい時 |

### prompts/ ディレクトリ

#### templates/ - プロンプトテンプレート

| ファイル | 用途 | 適している場合 |
|---------|------|--------------|
| `basic-api-spec.md` | 基本的なAPI仕様書 | 小規模API、初回作成 |
| `openapi-spec.md` | OpenAPI 3.0形式 | 標準規格準拠、ツール連携 |
| `endpoint-detail.md` | エンドポイント詳細 | 複雑なエンドポイント |
| `error-handling.md` | エラー処理仕様 | エラー処理の標準化 |

#### examples/ - 使用例

| ファイル | 内容 |
|---------|------|
| `user-management-api.md` | ユーザー管理APIの完全な例 |

### docs/ ディレクトリ

| ファイル | 用途 |
|---------|------|
| `usage-guide.md` | 詳細な使い方、ベストプラクティス、トラブルシューティング |

## ワークフロー

```
開始
  │
  ├─→ 初めて使う？
  │    └─→ YES → QUICKSTART.md を読む
  │    └─→ NO  → 次へ
  │
  ├─→ 何を作りたい？
  │    ├─→ 基本的なAPI仕様書      → templates/basic-api-spec.md
  │    ├─→ OpenAPI形式            → templates/openapi-spec.md
  │    ├─→ エンドポイント詳細     → templates/endpoint-detail.md
  │    └─→ エラーハンドリング     → templates/error-handling.md
  │
  ├─→ 使い方がわからない？
  │    └─→ YES → docs/usage-guide.md を読む
  │
  ├─→ 例を見たい？
  │    └─→ YES → examples/user-management-api.md を参照
  │
  └─→ 貢献したい？
       └─→ YES → CONTRIBUTING.md を読む
```

## 使用フロー図

```
┌─────────────────┐
│ 1. テンプレート │
│   を選択        │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ 2. カスタマイズ │
│   [...]を記入   │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ 3. AIエージェント│
│   に入力        │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ 4. 仕様書生成   │
│   完了！        │
└─────────────────┘
```

## テンプレート選択フローチャート

```
何を作りたいですか？
         │
         ├─→ 初めてAPI仕様書を作る
         │    └─→ basic-api-spec.md
         │
         ├─→ Swagger UIで表示したい
         │    └─→ openapi-spec.md
         │
         ├─→ 特定のエンドポイントを詳しく
         │    └─→ endpoint-detail.md
         │
         └─→ エラー処理を統一したい
              └─→ error-handling.md
```

## カスタマイズ度合い

```
テンプレート → カスタマイズ → AIエージェント → 仕様書

basic-api-spec.md
  └─ [API名]を記入
  └─ [エンドポイント]を記入
      └─ ChatGPT/Claude
          └─ Markdown形式の仕様書

openapi-spec.md
  └─ [API情報]を記入
  └─ [エンドポイント]を記入
      └─ ChatGPT/Claude
          └─ YAML形式のOpenAPI仕様書

endpoint-detail.md
  └─ [エンドポイント情報]を詳細に記入
      └─ ChatGPT/Claude
          └─ 詳細なエンドポイント仕様書

error-handling.md
  └─ [API情報]を記入
  └─ [エラーコード体系]を記入
      └─ ChatGPT/Claude
          └─ エラー処理仕様書
```

## ファイルサイズ目安

| ファイル | 行数 | 目的 |
|---------|-----|------|
| basic-api-spec.md | ~54行 | シンプルで使いやすい |
| openapi-spec.md | ~70行 | 標準形式に対応 |
| endpoint-detail.md | ~132行 | 最も詳細 |
| error-handling.md | ~95行 | エラー処理に特化 |

## 推奨される使用順序

### 初心者向け
1. `QUICKSTART.md` を読む
2. `templates/basic-api-spec.md` を使ってみる
3. `examples/user-management-api.md` を参考にする
4. 必要に応じて他のテンプレートを試す

### 経験者向け
1. 目的に合わせてテンプレートを直接選択
2. `docs/usage-guide.md` でベストプラクティスを確認
3. カスタマイズして使用

### 貢献者向け
1. `CONTRIBUTING.md` を読む
2. 既存のテンプレートを参考にする
3. 新しいテンプレートや例を追加

## まとめ

このリポジトリは、**プロンプト → AIエージェント → API仕様書** という流れで、
効率的に高品質なAPI仕様書を生成するためのツールキットです。

```
📚 学習       → README.md, QUICKSTART.md
🛠️ 使用       → prompts/templates/
📖 参考       → prompts/examples/, docs/usage-guide.md
🤝 貢献       → CONTRIBUTING.md
```
