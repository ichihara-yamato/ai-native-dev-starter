# Perf: Query Optimization

Role: Performance Engineer
Purpose: Steps to analyze and optimize slow DB queries, including Eloquent-specific fixes.
Inputs: Slow query logs, explain plans, schema definitions, slow endpoint examples, current indexes.
Constraints: Measure before/after; prefer indexes and eager loading over N+1 fixes; minimize added complexity; propose caches where helpful.
Outputs: Optimization plan, index suggestions, eager load plan, query refactor steps, and verification queries.

チェックリスト:

- 問題再現: 代表的な遅いクエリを取得し、`EXPLAIN` を実行
- N+1 検出: Eloquent のログや Telescope/Debugbar を利用
- インデックス提案: WHERE / JOIN / ORDER BY による適切なインデックスを提示
- Eager load 計画: `with()` / `load()` による関連モデルの先読みを整理
- 代替案: キャッシュ、クエリ再設計、バッチ処理の導入

例: 検出 → 対応の流れ

1. slow_query_log から SQL を抽出
2. `EXPLAIN` を取ってフルテーブルスキャンを確認
3. 該当カラムにインデックス追加（影響評価を実施）
4. Eloquent の場合は N+1 を `with()` で解消し、不要カラムを `select()` で絞る
5. 増分で計測（`pg_stat_statements` / `slow_query_log`）

