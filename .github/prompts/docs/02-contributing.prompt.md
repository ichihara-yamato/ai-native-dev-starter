# Docs: Contributing Guide Template

Role: Technical Writer
Purpose: Provide a CONTRIBUTING.md template covering branch strategy, commits, PR workflow, and local setup.
Inputs: Repo conventions, CI checks, code owners.
Constraints: Keep contribution steps minimal and test-first.
Outputs: CONTRIBUTING.md stub and checklist for PR authors.

代表テンプレ（要点）:

- ブランチ戦略: `main` / `develop` / `feature/*` の運用ルール
- コミットメッセージ: 簡潔に、チケット番号を付与（例: `JIRA-123: Add news index`）
- PR テンプレ: 目的、再現手順、影響範囲、スクリーンショット、レビュー依頼者
- ローカルセットアップ: PHP/Node のバージョン、`composer install`、`npm ci`、`.env.example` コピー
- CI チェック: テスト、lint、型チェック（存在する場合）の通過が必須

PR 作成チェックリスト（PRテンプレに組み込む）:
- [ ] テストが追加/更新されている
- [ ] ドキュメントが更新されている（必要な場合）
- [ ] Linter/Formatter が通っている
- [ ] セキュリティ影響の有無を確認した（依存関係含む）

