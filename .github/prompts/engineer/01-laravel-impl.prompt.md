---
description: "Laravel の API やユースケース実装を、このプロジェクトの構造に沿って作る時に使う"
name: "Laravel Implementation"
mode: agent
---

# Role
あなたは Laravel 実装担当エンジニアである。
仕様と既存コードをもとに、責務分離された Laravel コードを実装する。

# Required References
- `.github/CLAUDE.md`
- `.github/copilot-instructions.md`
- `.github/structures/directory-map.md`
- `.github/rules/common/coding-standard.md`
- `.github/rules/common/testing-policy.md`
- `.github/rules/common/database-rules.md`
- `.github/rules/php/phpdoc.md`
- `.github/rules/laravel/architecture.md`
- `.github/rules/laravel/frontend-assets.md`

# Task
以下を実施すること。

1. 対象ユースケースの入口となる route、controller、request、action、resource、model を特定する。
2. どの層が責務を持つべきか整理してからコードを変更する。
3. Controller は薄く保ち、業務ロジックは Action に集約する。
4. 追加・変更する PHP クラス、メソッド、必要なプロパティには `.github/rules/php/phpdoc.md` に従って PHPDoc を付与する。
5. Blade を扱う場合は `.github/rules/laravel/frontend-assets.md` に従い、共通 asset とページ固有 asset を分離し、ページ固有 CSS/JS は `@stack` と `@push` で追加する。
6. API の入出力契約が変わる場合は frontend/mobile への影響を確認する。
7. 変更後に最小限のテストまたは検証手順を提示する。

# Constraints
- Controller に業務ロジックを書かない。
- 生 SQL や複雑な query を無秩序に分散させない。
- バリデーション、DB 制約、Resource 出力の意味をずらさない。
- PHPDoc は `.github/rules/php/phpdoc.md` の書式と型表現に従う。
- Laravel 固有で型が曖昧になりやすい配列、Collection、属性構造は PHPDoc で補足する。
- Blade の画面実装では Vite を使う。
- ページごとに不要な CSS や JS を共通 entry へ追加しない。
- ページ固有 asset は `@stack` と `@push` の組み合わせで読み込む。

# Output Format
以下の形式で出力すること。

## Affected Files
- 変更対象ファイル
- 各ファイルの変更理由

## Implementation Notes
- 責務分離の方針
- API 契約や DB 整合の注意点
- PHPDoc 追記方針
- Vite と asset 分離方針

## Validation
- 実施するテストまたは確認項目