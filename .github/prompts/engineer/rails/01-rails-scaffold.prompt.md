# Engineer: Rails Scaffold

Role: Engineer
Purpose: Generate routes / controller / service / serializer / model skeletons from a feature spec.
Inputs: Feature description, entities, auth requirements, API vs HTML response.
Constraints: Follow `app/services/` pattern and Strong Parameters rules; see `.github/rules/rails/architecture.md`.
Outputs: File list with minimal code stubs, responsibilities, and Laravel-equivalent mapping.

スキャフォールド対応表（Laravel → Rails）:

| Laravel | Rails |
|---------|-------|
| `app/Http/Controllers/` | `app/controllers/` |
| `app/Actions/` | `app/services/` |
| `app/Http/Requests/` | Strong Parameters (controller 内) |
| `app/Http/Resources/` | `app/serializers/` または jbuilder |
| `app/Models/` | `app/models/` |
| `routes/api.php` | `config/routes.rb` |

生成チェックリスト:

- `config/routes.rb` にリソースルートを追加
- `app/controllers/` にコントローラーを生成（薄く保つ）
- `app/services/` にサービスクラスを作成（業務ロジックを集約）
- `app/models/` にバリデーションとアソシエーションを定義
- `app/serializers/` または jbuilder ビューで JSON レスポンスを整形
- `spec/requests/` または `spec/services/` にテストスケルトンを追加
