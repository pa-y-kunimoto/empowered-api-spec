# REST API仕様書 拡充指示 - E-Commerce API例

以下のOpenAPI仕様書（YAML形式）をもとに、説明内容が充実したAPI仕様書を作成してください。

---

## 🎯 目的

このドキュメントの目的は、**API利用者がAPIの構造・意味・利用手順を明確に理解できる仕様書を生成すること**です。  
単なるリファレンスではなく、**ユースケース中心・手順中心のドキュメント**としてください。

---

## 🧩 出力構成

出力は以下の構成で生成してください。

### 1. API全体概要
- システム全体の目的や想定ユースケースをわかりやすく説明する。
- 想定ユースケースごとに、どのAPIをどの順番で呼び出すかを**手順として列挙**する。
  - 各手順にはAPI名（`summary`の値）とHTTPメソッド＋エンドポイントを併記する。
  - 可能であれば簡単なリクエスト／レスポンス例を示す。

### 2. API詳細仕様
APIごとに以下の情報をまとめる。

#### フォーマット
- **{summary}（{HTTPメソッド} {path}）**
- 概要
- 用語定義
- リクエスト仕様
- レスポンス仕様
- 関連API・利用手順

---

## 📦 入力データ

以下にOpenAPI仕様書をYAML形式で埋め込みます。

```yaml
openapi: 3.0.0
info:
  title: E-Commerce API
  version: 1.0.0
  description: オンラインショッピングサイトのバックエンドAPI

servers:
  - url: https://api.example.com/v1
    description: 本番環境

paths:
  /auth/login:
    post:
      summary: ユーザー認証
      description: ユーザーIDとパスワードで認証し、アクセストークンを取得
      tags:
        - 認証
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                email:
                  type: string
                  format: email
                password:
                  type: string
                  format: password
              required:
                - email
                - password
      responses:
        '200':
          description: 認証成功
          content:
            application/json:
              schema:
                type: object
                properties:
                  access_token:
                    type: string
                  user_id:
                    type: string
        '401':
          description: 認証失敗

  /users/{id}:
    get:
      summary: ユーザー情報取得
      description: 指定したIDのユーザー情報を取得
      tags:
        - ユーザー
      parameters:
        - name: id
          in: path
          required: true
          schema:
            type: string
      responses:
        '200':
          description: 成功
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'
        '404':
          description: ユーザーが見つかりません

  /items:
    get:
      summary: 商品一覧取得
      description: 商品の一覧を取得します。ページネーション対応。
      tags:
        - 商品
      parameters:
        - name: page
          in: query
          schema:
            type: integer
            default: 1
        - name: limit
          in: query
          schema:
            type: integer
            default: 20
        - name: category
          in: query
          schema:
            type: string
      responses:
        '200':
          description: 成功
          content:
            application/json:
              schema:
                type: object
                properties:
                  items:
                    type: array
                    items:
                      $ref: '#/components/schemas/Item'
                  total:
                    type: integer
                  page:
                    type: integer

  /items/{id}:
    get:
      summary: 商品詳細取得
      description: 指定したIDの商品詳細を取得
      tags:
        - 商品
      parameters:
        - name: id
          in: path
          required: true
          schema:
            type: string
      responses:
        '200':
          description: 成功
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Item'
        '404':
          description: 商品が見つかりません

  /cart:
    post:
      summary: カート追加
      description: カートに商品を追加
      tags:
        - カート
      security:
        - bearerAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                item_id:
                  type: string
                quantity:
                  type: integer
              required:
                - item_id
                - quantity
      responses:
        '200':
          description: 追加成功
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Cart'
        '401':
          description: 認証が必要です

  /orders:
    post:
      summary: 購入確定
      description: カート内の商品を購入
      tags:
        - 注文
      security:
        - bearerAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                payment_method:
                  type: string
                  enum: [credit_card, bank_transfer]
                shipping_address_id:
                  type: string
              required:
                - payment_method
                - shipping_address_id
      responses:
        '201':
          description: 注文完了
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Order'
        '401':
          description: 認証が必要です
        '400':
          description: カートが空です

components:
  schemas:
    User:
      type: object
      properties:
        id:
          type: string
        email:
          type: string
        name:
          type: string

    Item:
      type: object
      properties:
        id:
          type: string
        name:
          type: string
        price:
          type: number
        description:
          type: string
        stock:
          type: integer

    Cart:
      type: object
      properties:
        items:
          type: array
          items:
            type: object
            properties:
              item_id:
                type: string
              quantity:
                type: integer
        total_price:
          type: number

    Order:
      type: object
      properties:
        order_id:
          type: string
        user_id:
          type: string
        items:
          type: array
          items:
            type: object
        total_price:
          type: number
        status:
          type: string

  securitySchemes:
    bearerAuth:
      type: http
      scheme: bearer
```

---

## 🏁 出力形式

最終出力はMarkdown形式の仕様書として、以下の構成順で作成すること。

1. **API全体概要**（ユースケース＋呼び出し手順一覧）
2. **各APIの詳細仕様**（summary順またはカテゴリ順）
