# AGENTS.md

## Overview
マルチプラットフォーム構成のプロジェクト。以下のスタックに対応する。
- Backend: Laravel (PHP 8.2+)
- Frontend: TypeScript + React / Vue 3
- Mobile: Flutter (Dart)
- Automation: Python
- Alternate backend: Ruby on Rails

## Repository Structure
`.github/structures/directory-map.md` に完全なディレクトリマップが定義されている。

| Layer | Root path | Notes |
|-------|-----------|-------|
| Backend (Laravel) | `app/` | Controllers, Actions, Models, Resources |
| Frontend | `frontend/` | TypeScript, React or Vue 3 |
| Mobile | `mobile/` | Flutter / Dart |
| Automation | `automation/` | Python scripts and models |

## Rules
コード生成前に対象スタックのルールファイルを必ずロードすること。

| 対象 | ルールファイル |
|------|---------------|
| 全スタック共通 | `.github/rules/common/coding-standard.md` |
| 全スタック共通 | `.github/rules/common/testing-policy.md` |
| DB 変更時 | `.github/rules/common/database-rules.md` |
| Laravel | `.github/rules/laravel/architecture.md` |
| Laravel assets | `.github/rules/laravel/frontend-assets.md` |
| PHP / Laravel | `.github/rules/php/coding-standard.md` |
| PHP / Laravel | `.github/rules/php/phpdoc.md` |
| TypeScript | `.github/rules/typescript/base-rules.md` |
| React | `.github/rules/typescript/react-patterns.md` |
| Vue 3 | `.github/rules/typescript/vue-patterns.md` |
| Flutter | `.github/rules/flutter/dart-style.md` |
| Flutter state | `.github/rules/flutter/state-management.md` |
| Python (自動化・スクレイピング) | `.github/rules/python/automation.md` |
| Python (ETL・パイプライン) | `.github/rules/python/data-pipeline.md` |
| Python (API・モデルサービング) | `.github/rules/python/api-serving.md` |
| Rails | `.github/rules/rails/architecture.md` |
| Rails testing | `.github/rules/rails/testing.md` |

## Workflow
1. タスク内容から対象レイヤーとスタックを判断する。
2. 上記ルールテーブルから該当ファイルを読み込む。
3. コード出力前に以下を提示して承認を得ること。
   - **Stack**: 特定したスタック
   - **Role**: Engineer / Architect / Reviewer など
   - **Rules**: 適用するルールファイル一覧
   - **Actions**: 操作するファイルと目的
4. クロススタック変更の場合は API 型の整合性を確認する。

## Available Prompts
`.github/prompts/` に役割別・スタック別のプロンプトが用意されている。
スキャフォールディングやレビュー時はまずこのディレクトリを確認する。

## API Contract
`.github/doc_formats/api-spec-template.md` が API スキーマの正本。
バックエンドのレスポンス変更時は `frontend/src/api/` と `mobile/lib/services/` を同時に更新する。

## Testing
テストの観点と最低基準は `.github/rules/common/testing-policy.md` を参照。
検証できなかった項目は成果物に明記すること。
