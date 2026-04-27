# DevOps: CI Smoke Plan

Role: DevOps
Purpose: Define a minimal CI smoke pipeline to validate PHP and frontend builds.
Inputs: Repo language, build commands, test commands.
Constraints: Keep runtime under 10 minutes; cache dependencies.
Outputs: Workflow skeleton and recommended runners.

代表ワークフロー（短縮版）:

```yaml
name: CI Smoke
on: [push, pull_request]
jobs:
	smoke:
		runs-on: ubuntu-latest
		steps:
			- uses: actions/checkout@v4
			- uses: shivammathur/setup-php@v2
				with:
					php-version: 8.2
			- name: Setup node
				uses: actions/setup-node@v4
				with: node-version: 18
			- name: Cache composer
				uses: actions/cache@v4
				with: path: ~/.composer/cache
			- name: Install PHP deps
				run: composer install --no-progress --no-suggest --prefer-dist
			- name: Install node deps
				run: npm ci
			- name: Build assets
				run: npm run build --if-present
			- name: Run phpunit
				run: composer test --no-interaction
```

最小実行チェックリスト:
- `composer install` が成功する
- `npm ci` と `npm run build` が成功する（Vite manifest が生成される）
- マイグレーション／シーディングはスキップ可（時間短縮）だが、seed 用オプションを用意
- `phpunit --filter smoke` のようなスモークテストセットを用意して短時間で検証

キャッシュ/並列化の提案:
- Composer キャッシュ、node_modules キャッシュを利用
- フロントエンドとバックエンドを並列ジョブで実行して時間短縮

