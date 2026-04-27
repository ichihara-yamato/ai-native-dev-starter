# Python API Serving Rules

## Purpose
- FastAPI / Flask を使ったモデルサービングおよび API サーバー実装のルールを定義する。
- スクリプト全般のルールは `.github/rules/python/automation.md` を参照する。

## Framework Choice
- 新規実装は FastAPI を優先する（型安全・自動ドキュメント・async 対応）。
- 既存 Flask プロジェクトへの追加は Flask で統一し、混在させない。

## Request / Response Schema
- リクエストとレスポンスは Pydantic モデルで定義し、`dict` のまま受け渡さない。
- レスポンスモデルは `response_model` に明示し、意図しないフィールドの漏洩を防ぐ。
- エラーレスポンスは `{"error": {"code": "string", "message": "string"}}` 形式に統一する。
- 日付・時刻は ISO 8601 形式（UTC）で返す。

## Endpoint Design
- 1 エンドポイントは 1 責務に限定し、複数の処理を詰め込まない。
- 副作用のある処理（書き込み・更新・削除）は POST / PUT / PATCH / DELETE を使い、GET に副作用を持たせない。
- バリデーションエラーは 422、認証エラーは 401、権限エラーは 403 で返す。

## Model Loading
- ML モデルはアプリ起動時に一度だけロードし、シングルトンとして保持する。
- リクエストごとにモデルをロードしない（レイテンシとメモリの浪費）。
- モデルファイルのパスは環境変数または設定ファイルで管理し、コードにハードコードしない。

## Async And Performance
- I/O バウンドな処理（DB・外部 API・ファイル読み書き）は `async def` で実装する。
- CPU バウンドな推論処理は `asyncio.run_in_executor` で別スレッドに委譲する。
- バッチ推論が有効な場合は、複数リクエストをまとめて処理できる設計を検討する。

## Health And Observability
- `GET /health` エンドポイントを必ず実装し、モデルのロード状態・依存サービスの疎通を返す。
- リクエストごとにリクエスト ID をログに含め、トレーサビリティを確保する。
- レスポンスタイム・エラー率をログまたはメトリクスとして記録する。

## Configuration And Secrets
- 環境変数は `pydantic-settings` の `BaseSettings` で一元管理する。
- API キー・DB 接続情報をコードや出力ログに含めない。
- 開発・ステージング・本番で設定を切り替えられるようにする。
