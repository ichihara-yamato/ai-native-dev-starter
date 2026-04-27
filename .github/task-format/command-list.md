# Command List

## Purpose
- ユーザーが `コマンド` として依頼したときの標準フローを定義する。
- AI は自由入力の都度解釈ではなく、この一覧に従って作業を開始する。

## Common Flow
すべてのコマンドで以下を実施すること。

1. `.github/structures/directory-map.md` を参照して影響範囲を特定する。
2. 対象技術スタックに対応する `.github/rules/` を読み込む。
3. 必要に応じて `.github/prompts/` と `.github/doc_formats/` を参照する。
4. 作業計画を提示してから成果物作成または修正に入る。
5. 実装系コマンドでは、変更後に最小限の検証を行う。

## Command Definitions

### コマンド: 要件→仕様
- 目的: 要件、議事メモ、モックから仕様書の叩き台を作成する。
- 主担当: Designer
- 主な参照:
	- `.github/prompts/designer/01-requirements-to-spec.prompt.md`
	- `.github/doc_formats/api-spec-template.md`
- 主な成果物:
	- `docs/` 配下の仕様書
	- API を含む場合は API 仕様書
- 必須観点:
	- スコープ
	- 入力、出力、エラー条件
	- 権限、非機能、例外系

### コマンド: 仕様→構造
- 目的: 仕様からファイル構成、責務分割、実装単位を設計する。
- 主担当: Architect
- 主な参照:
	- `.github/prompts/architect/01-spec-to-structure.prompt.md`
	- `.github/structures/directory-map.md`
- 主な成果物:
	- 実装対象ファイル一覧
	- 役割分担メモ
	- 必要な仕様差分
- 必須観点:
	- 層の責務分離
	- API 契約の整合
	- 実装順序

### コマンド: Laravel実装
- 目的: Laravel の API、Action、Model、Resource を実装または修正する。
- 主担当: Engineer
- 主な参照:
	- `.github/prompts/engineer/01-laravel-impl.prompt.md`
	- `.github/rules/laravel/architecture.md`
- 主な成果物:
	- `app/`, `routes/` 配下のコード
	- 必要に応じてテストコード
- 必須観点:
	- Controller を薄く保つ
	- Action への責務集約
	- frontend/mobile への API 影響確認

### コマンド: PHP実装
- 目的: 将来の Laravel 以外も含む PHP コードを、共通 PHPDoc ルール込みで実装または修正する。
- 主担当: Engineer
- 主な参照:
	- `.github/prompts/engineer/00-php-impl.prompt.md`
	- `.github/rules/php/phpdoc.md`
	- 対象フレームワーク固有の rule
- 主な成果物:
	- 対象 PHP フレームワーク配下のコード
	- 必要に応じてテストコード
- 必須観点:
	- ネイティブ型と PHPDoc の整合
	- PHPStan を意識した配列、複合型の補足
	- フレームワーク固有の責務分離

### コマンド: Python実装
- 目的: automation 配下のスクリプト、モデル、出力処理を実装または修正する。
- 主担当: Engineer
- 主な参照:
	- `.github/prompts/engineer/02-python-impl.prompt.md`
	- `.github/rules/python/automation.md`
- 主な成果物:
	- `automation/scripts/`, `automation/models/` 配下のコード
	- 必要に応じて出力仕様
- 必須観点:
	- timeout、retry、再実行性
	- logs/output の分離
	- モデル定義の明確化

### コマンド: TypeScript実装
- 目的: frontend 配下の TypeScript 実装を行う。
- 主担当: Engineer
- 主な参照:
	- `.github/prompts/engineer/03-typescript-impl.prompt.md`
	- `.github/rules/typescript/base-rules.md`
	- 必要に応じて React または Vue の rule
- 主な成果物:
	- `frontend/src/components/`, `frontend/src/hooks/`, `frontend/src/composables/`, `frontend/src/api/`, `frontend/src/types/`
- 必須観点:
	- 型安全性
	- API 契約整合
	- loading、error、empty state

### コマンド: Flutter実装
- 目的: Flutter の UI、状態管理、サービス、モデルを実装または修正する。
- 主担当: Engineer
- 主な参照:
	- `.github/prompts/engineer/04-flutter-impl.prompt.md`
	- `.github/rules/flutter/dart-style.md`
	- `.github/rules/flutter/state-management.md`
- 主な成果物:
	- `mobile/lib/ui/`, `mobile/lib/providers/` または `bloc/`, `mobile/lib/services/`, `mobile/lib/models/`
- 必須観点:
	- UI と状態管理の分離
	- API 契約整合
	- 失敗時状態の扱い

### コマンド: Rails実装
- 目的: Rails の routes、Controller、Service Object、Serializer、Model を実装または修正する。
- 主担当: Engineer
- 主な参照:
	- `.github/prompts/engineer/05-rails-impl.prompt.md`
	- `.github/rules/rails/architecture.md`
- 主な成果物:
	- `app/controllers/`, `app/services/`, `app/models/`, `app/serializers/` 配下のコード
	- 必要に応じてテストコード
- 必須観点:
	- Controller を薄く保ち業務ロジックを Service Object に集約
	- Strong Parameters の適用
	- N+1 クエリの排除
	- frontend/mobile への API 影響確認

### コマンド: レビュー
- 目的: 変更内容を仕様、規約、構造、試験観点の観点からレビューする。
- 主担当: Reviewer
- 主な参照:
	- `.github/prompts/reviewer/01-code-review.prompt.md`
	- `.github/rules/common/*.md`
	- 対象スタックの rule
- 主な成果物:
	- 指摘一覧
	- 未確定事項
	- 残留リスク
- 必須観点:
	- 重大度順の指摘
	- 根拠と影響の明示
	- テスト観点漏れの確認
	- PHP ファイルを含む場合の PHPDoc と型情報の妥当性

### コマンド: 問題票作成
- 目的: 不具合、レビュー指摘、改善課題を再利用可能な形式で記録する。
- 主担当: Reviewer または Designer
- 主な参照:
	- `.github/doc_formats/issue-template.md`
- 主な成果物:
	- 問題票、指摘票、改善依頼
- 必須観点:
	- 再現条件
	- 期待結果と実際結果
	- 影響範囲
	- 優先度

## Interpretation Rules
- コマンド名が部分一致する場合は、より具体的なものを優先する。
- スタック横断の依頼は、共通 rule と関係する複数 stack の rule を併用する。
- コマンドが未定義でも、既存コマンドに近い目的なら近いフローを提案する。
- 未定義コマンドを繰り返し使う場合は、このファイルへの追加を検討する。
