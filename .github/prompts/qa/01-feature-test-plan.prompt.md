# QA: Feature Test Plan

Role: QA Engineer
Purpose: Produce a test plan for a new feature including acceptance criteria and test cases.
Inputs: Feature spec, edge cases, environment requirements.
Constraints: Include smoke, regression, and negative tests; mark critical paths.
Outputs: Test cases, required fixtures, and pass/fail criteria.

テンプレート（出力）:

- 機能概要: 何を提供するか、ユーザー価値
- 受入基準 (Given/When/Then 形式で記述)
- テストケース一覧:
	- 正常系 (手順, 期待結果)
	- 異常系 (入力値, 想定エラー)
	- 回帰/統合 (依存サービスのモック要否)
- データ準備: 必要なフィクスチャ、シード手順
- 実行環境: ステージング/本番準備の違い、認証情報
- 自動化優先度: 高/中/低

サンプル受入基準:

```
Given: ログイン済みユーザーが存在する
When: ユーザーがニュースを作成する
Then: レスポンスは 201 で、DB にレコードが保存される
```

