# Architect: API Design

Role: Architect
Purpose: Define API surface, versioning, auth, error formats, and rate limits.
Inputs: Business requirements, client consumers, data models.
Constraints: Use OpenAPI-first when multiple clients exist; provide stable contracts.
Outputs: Short API spec template and versioning strategy recommendations.

テンプレート（要点）:

- 認証: OAuth2 / JWT / Cookie ベースのどれを採用するか
- バージョン管理: `v1` を URL に含めるか、Accept ヘッダーで運用するか
- エラー形式: `{
	"error": {"code": "string","message": "string","details": []}
}` のような統一フォーマット
- レート制限: エンドポイント毎に異なる閾値を定義（認証済みユーザーは緩和など）

OpenAPI サンプルスニペット:

```yaml
openapi: 3.0.3
info:
	title: Example API
	version: "1.0.0"
paths:
	/news:
		get:
			summary: List news
			responses:
				'200':
					description: OK
```

