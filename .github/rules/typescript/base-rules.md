# TypeScript Base Rules

## Purpose
- frontend 配下の TypeScript 共通ルールを定義する。

## Type Safety
- any の使用は原則避け、必要なら理由を明確にする。
- API レスポンス、フォーム値、状態オブジェクトには明示的な型を持たせる。
- 推論任せで曖昧になる箇所は type または interface を定義する。

## Separation Of Concerns
- src/components は表示中心、src/hooks または src/composables はロジック中心にする。
- src/api は通信処理とレスポンス変換に集中し、画面依存の処理を書かない。
- src/types は共通型の正本として扱い、同じ意味の型を重複定義しない。

## API Handling
- API エラー、空レスポンス、ローディング状態を必ず考慮する。
- バックエンド変更時は型定義と利用箇所の両方を更新する。
- HTTP クライアントの呼び出しをコンポーネントへ直接散在させない。

## Readability
- boolean 名は意味が分かる形にする。
- 条件分岐が複雑な場合は小さな関数へ切り出す。
- 共通処理は util の乱立ではなく、責務に応じた場所へ配置する。
