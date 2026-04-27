# Review: Code Style

Role: Reviewer
Purpose: Checklist for linting, formatting, and style rules for PRs.
Inputs: Repo language, existing lint rules.
Constraints: Prefer automated fixes via CI.
Outputs: Pass/fail checklist and auto-fix commands.

チェックリスト（重要項目）:

- 自動フォーマッタ: `php-cs-fixer` / `prettier` が実行されているか
- 依存関係の変更でスタイルルールが壊れていないか
- PSR-12 / プロジェクト固有ルールの逸脱がないか
- 不要なワイルドカードインポートや未使用変数がないか

レビューワークフロー:

1. ローカルで自動整形を一度実行する:

```bash
composer run php-cs-fixer fix
npm run prettier --write "resources/**/*.js"
```

2. CI上でのチェックコマンド（例）:

```yaml
run: composer run php-cs-fixer -- --diff --check
```

3. 自動修正可能な差分は PR にコメントして修正を要求するか、PR 作者に自動fixを実行してもらう。

備考:
- 大きなスタイル差分は別の PR に分割してレビューしやすくする。

