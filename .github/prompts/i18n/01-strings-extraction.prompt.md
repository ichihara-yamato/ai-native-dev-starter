# I18n: Strings Extraction

Role: Localization Engineer
Purpose: Provide a plan to extract strings and prepare localization pipeline.
Inputs: Source code, templating language, existing translations.
Constraints: Keep keys stable, avoid string interpolation in keys.
Outputs: Extraction steps, key naming guideline, PO/JSON output example.

ワークフロー:

1. ソース走査: `grep`/`xgettext`/抽出スクリプトで translatable strings を抽出
2. キー付け規約: `namespace.section.key` 形式を推奨（例: `news.list.title`）
3. CI 統合: 文字列差分を検出して翻訳キーの欠落を CI で警告
4. 出力形式: PO / JSON / XLIFF をサポート

注意点:
- HTML テンプレート内の変数結合は避け、プレースホルダ（`:name`）を使う
- 多言語対応で日付/数値フォーマットはローカル化層で処理

