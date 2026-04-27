# Rails Testing Rules

## Purpose
- Rails 実装時のテスト記述規約を定義する。
- テストの観点と最低基準は `.github/rules/common/testing-policy.md` を参照する。
- 本ファイルは RSpec / FactoryBot を前提とした Rails 固有の記述ルールを定める。

## File Structure
- `spec/requests/` に API エンドポイントの統合テストを置く。
- `spec/models/` にバリデーション・アソシエーション・スコープのテストを置く。
- `spec/services/` に Service Object のユニットテストを置く。
- `spec/factories/` に FactoryBot のファクトリ定義を置く。
- `spec/support/` に共通ヘルパーや shared_examples を置く。

## Describe / Context / It
- `describe` にはクラス名またはメソッド名（`#instance_method`, `.class_method`）を書く。
- `context` には条件を書き、`when` / `with` / `without` で始める。
- `it` には期待する振る舞いを書き、`should` は使わず現在形で書く（例: `returns 200`）。
- ネストは 3 階層を超えないようにする。

## FactoryBot
- ファクトリは最小限の必須属性だけ定義し、オプション属性は trait で拡張する。
- テストごとに `create` / `build` / `build_stubbed` を使い分け、DB 不要なら `build` を優先する。
- 本番データに近い現実的な値を使い、`"test"` や `1` だけのダミー値を並べない。
- 関連モデルが必要な場合は association を使い、ファクトリ内で直接 create しない。

## Let And Subject
- テストデータは `let` で遅延評価し、`before` ブロックでの冗長な代入を避ける。
- 即時評価が必要な場合のみ `let!` を使う。
- `subject` には「このテストで検証する主な操作」を置き、`is_expected.to` で簡潔に書く。

## Request Specs
- HTTP メソッド・パス・ヘッダー・ボディを明示して呼び出す。
- レスポンスのステータスコード・JSON 構造・DB 状態の 3 点を確認する。
- 認証が必要なエンドポイントは認証済み / 未認証の両方をテストする。
- 異常系（不正パラメーター・権限不足・存在しないリソース）を省略しない。

## Mocking And Stubbing
- 外部 API やメール送信など外部 I/O は `allow(...).to receive` でスタブする。
- `expect(...).to receive` はメッセージ送信自体を検証するときに限定する。
- DB を伴うテストでは `DatabaseCleaner` または `use_transactional_fixtures` を使う。
- 実装の内部詳細（private メソッド）をテストするより、公開 API 経由で検証する。
