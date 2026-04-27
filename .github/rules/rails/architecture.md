# Rails Architecture Rules

## Purpose
- Rails 実装時の責務分離と配置ルールを定義する。
- Laravel の `rules/laravel/architecture.md` に対応する Rails 固有の規約。

## Layer Responsibilities
- Controllers はリクエスト受領、Strong Parameters 適用、レスポンス返却に限定する。
- Service Objects はビジネスロジックを 1 ユースケース 1 クラスで担当する。
- Models は永続化、バリデーション、リレーション、スコープに責務を限定する。
- Serializers は JSON レスポンス整形のみを担当し、業務判断を入れない。
- routes.rb ではエンドポイント定義に集中し、詳細ロジックを書かない。

## Request And Validation
- Strong Parameters を必ず使い、ホワイトリスト外のパラメーターを通さない。
- モデルバリデーションと Strong Parameters の役割を混同しない。
- バリデーションはモデル側に定義し、コントローラーで重複検証しない。

## Service Objects
- `app/services/` にユースケース単位のサービスクラスを配置する。
- サービスは単一責務とし、1 クラスが複数のユースケースを担当しない。
- サービスの成功/失敗は Result パターンまたは例外で表現し、boolean だけで返さない。
- 他サービスの多段ネストで流れを不透明にしない。

## ActiveRecord Usage
- N+1 を避けるため `includes` / `eager_load` / `preload` を適切に使う。
- スコープは再利用頻度の高いクエリ条件に限定し、巨大なスコープを作らない。
- fat model は Concerns や Service Objects で分割する。
- 生 SQL は ActiveRecord で表現困難な場合に限定し、SQL インジェクションに注意する。

## API Consistency
- Serializer の出力項目は frontend/mobile が利用する契約として扱う。
- エラー形式、HTTP ステータス、ページネーション形式は既存 API に合わせる。
- 仕様変更時は `frontend/src/api/` と `mobile/lib/services/` への影響を確認する。

## Testing
- RSpec または Minitest を利用し、FactoryBot でテストデータを準備する。
- Request spec（統合）と unit spec（Service/Model）を使い分ける。
- テストデータに実在の個人情報や機密情報を使わない。
