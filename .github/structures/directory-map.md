# Project Directory Map (Multi-Platform Architecture)

このプロジェクトは、Web（Laravel/React/Vue）、モバイル（Flutter）、自動化（Python）が統合されたマルチプラットフォーム構成です。AIはファイル操作時、以下の構造とルールを厳守してください。

## 1. Backend Layer (Laravel)
- **`app/`**:
    - `Http/Controllers/`: リクエスト受領とレスポンス返却のみ。ロジック禁止。
    - `Actions/`: ビジネスロジック（1ユースケース1クラス、`__invoke`形式）。
    - `Models/`: Eloquentモデル、リレーション、スコープ。
    - `Resources/`: APIリソース（JSON変換ロジック）。
- **`routes/api.php`**: フロントエンド・モバイル向けのAPI定義。
- **`storage/logs/`**: Laravel専用のアプリケーションログ出力先。

## 2. Frontend Layer (TypeScript / React / Vue)
- **`frontend/`**: 
    - `src/components/`: UIコンポーネント。
    - `src/hooks/` (React) / `src/composables/` (Vue): ロジックの共通化。
    - `src/api/`: Backend APIを呼び出すクライアント定義（Axios/Fetch）。
    - `src/types/`: TypeScriptの型定義ファイル。
- **`frontend/logs/`**: 開発時、またはSSR（Next.js/Nuxt.js等）利用時のフロントエンド用ログ。

## 3. Mobile Layer (Flutter / Dart)
- **`mobile/`**:
    - `lib/models/`: データ構造定義。
    - `lib/providers/` (or `bloc/`): 状態管理ロジック。
    - `lib/services/`: API通信クラス。
    - `lib/ui/`: スクリーンおよびウィジェット。
- **`mobile/logs/`**: デバッグ実行時のログおよびクラッシュレポート等。

## 4. Automation & AI Layer (Python)
- **`automation/`**: 
    - `scripts/`: Playwright等を用いた自動化エントリーポイント。
    - `models/`: Pydanticを用いたデータ型定義。
    - `output/`: スクレイピング結果、スクショ、PDF等の生成物。
    - `logs/`: Pythonスクリプト専用の実行ログ。

## 5. Shared Resources & Documentation
- **`docs/`**: 要件定義、API仕様書（Swagger/OpenAPI）、DB設計図。
- **`.github/`**:
    - `rules/`: 言語・スタック別のAI用規約。
    - `prompts/`: 職能（Role）別のAI用プロンプト。
    - `doc_formats/`: 成果物のテンプレート。

---
**🚨 AIへの厳格な指示（Strict Directives）:**
1. **コンテキストの分離**: 
   Laravelのロジックを `mobile/` に書いたり、Pythonのログを `storage/` に出力したりすることを厳禁とします。必ず上記マップに従ってください。
2. **APIの整合性**: 
   Backendを変更する場合は必ず `frontend/src/api/` および `mobile/lib/services/` への影響を確認し、必要に応じて同期的な修正案を提示してください。
3. **作業計画への反映**: 
   レスポンス開始時の「作業計画」には、どのディレクトリ（Backend/Frontend/Mobile/Automation）のファイルを操作するかを明記してください。