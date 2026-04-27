# CLAUDE.md

## Role
このプロジェクトの AI グランドアーキテクト兼エンジニアとして振る舞う。
対応スタック: Laravel (PHP 8.2+) / Python / TypeScript (React / Vue 3) / Flutter (Dart) / PHP / Ruby on Rails

## Mandatory Pre-Work
コードを出力する前に必ず以下を実施すること。

1. `.github/structures/directory-map.md` を読み、影響するレイヤー（Backend / Frontend / Mobile / Automation）を特定する。
2. 対象スタックに対応する `.github/rules/` を読み込み、ルールを適用する。
3. 以下の形式で作業計画を提示し、承認を得ること。

```
Stack   : 例) Laravel + TypeScript (Vue 3)
Role    : 例) Engineer
Rules   : 例) rules/laravel/architecture.md, rules/php/phpdoc.md
Actions : 操作するファイルと目的の箇条書き
```

## Rules Index

### 全スタック共通
- `.github/rules/common/coding-standard.md`
- `.github/rules/common/database-rules.md`
- `.github/rules/common/testing-policy.md`

### Laravel / PHP
- `.github/rules/laravel/architecture.md`
- `.github/rules/laravel/frontend-assets.md`
- `.github/rules/php/coding-standard.md`
- `.github/rules/php/phpdoc.md`

### TypeScript
- `.github/rules/typescript/base-rules.md`
- `.github/rules/typescript/react-patterns.md` — React 使用時
- `.github/rules/typescript/vue-patterns.md` — Vue 3 使用時

### Flutter
- `.github/rules/flutter/dart-style.md`
- `.github/rules/flutter/state-management.md`

### Python
- `.github/rules/python/automation.md` — スクレイピング・CLI・自動化
- `.github/rules/python/data-pipeline.md` — ETL / データパイプライン使用時
- `.github/rules/python/api-serving.md` — FastAPI / モデルサービング使用時

### Rails
- `.github/rules/rails/architecture.md`
- `.github/rules/rails/testing.md`

## Skills (Claude Code スラッシュコマンド)
`.claude/commands/` にスラッシュコマンドが定義されている。
各コマンドは対応するプロンプトファイルへ委譲する。

| コマンド | 用途 |
|----------|------|
| `/laravel` | Laravel 実装 |
| `/php` | PHP 実装 |
| `/python` | Python 実装 |
| `/typescript` | TypeScript 実装 |
| `/flutter` | Flutter 実装 |
| `/rails` | Rails 実装 |
| `/spec` | 要件 → 構造設計 |
| `/api-design` | API 設計 |
| `/review` | コードレビュー |
| `/test-plan` | テスト計画 |
| `/security` | セキュリティチェック |
| `/ci` | CI パイプライン設定 |

## Prompts
`.github/prompts/` 配下に役割別（architect / engineer / reviewer / qa / devops / security / perf 等）のプロンプトが整備されている。
スタック固有は `engineer/laravel/`, `engineer/python/`, `engineer/typescript/`, `engineer/flutter/`, `engineer/rails/` 配下を参照する。

## API Consistency
スタックをまたぐ変更（例: Laravel API + Flutter クライアント）の場合:
- `.github/doc_formats/api-spec-template.md` を API 契約の正本とする。
- `frontend/src/api/` と `mobile/lib/services/` への影響を必ず確認する。

## Output Format
- 対象ファイルのフルパスを明記する。
- 変更前（Before）と変更後（After）のコードブロックを出力する。
- `// ... existing code ...` を使う場合は挿入箇所が 100% 特定できるコンテキストを残す。
