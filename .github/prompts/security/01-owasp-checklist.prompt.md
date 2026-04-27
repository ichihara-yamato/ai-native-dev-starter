# Security: OWASP Checklist

Role: Security Engineer
Purpose: Map feature surfaces to OWASP Top 10 checks and remediation suggestions.
Inputs: Authentication model, inputs from users, file uploads.
Constraints: Prioritize critical vulnerabilities and quick mitigations.
Outputs: Checklist and remediation steps.

主要チェック項目:

- 入力バリデーション: SQLインジェクション、コマンドインジェクション、XSS の確認
- 認可/認証: 不適切な権限付与やIDORがないか
- セッション管理: セッショントークンの取り扱い、Secure/HttpOnly の設定
- シークレット管理: `.env` の誤コミット、ハードコードされたAPIキーの検出
- 依存関係: `composer audit` / `npm audit` による脆弱性検出と優先度付け

実行手順（PRレビューワークフロー）:
1. 自動スキャン：依存関係スキャン、SAST（例: GitHub CodeQL）を実行
2. 手動チェック：セキュリティに敏感な箇所（認証、アップロード、ファイル処理）を重点レビュー
3. 軽微な問題は自動修正を提案、重大問題は修正必須でPR保留

出力サンプル: 脆弱性カテゴリ、影響範囲、修正案、緊急度（Critical/High/Medium/Low）
