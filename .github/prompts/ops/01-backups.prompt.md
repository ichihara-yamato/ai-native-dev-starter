# Ops: Backups & Restore

Role: Operations
Purpose: Backup strategies for DB and uploaded assets, and restore steps.
Inputs: DB size, storage provider, retention policy.
Constraints: Test restores regularly; encrypt backups at rest and in transit.
Outputs: Backup schedule, restore playbook, and verification commands.

ベーシック手順:

1. DB バックアップ: 毎日夜間にフルバックアップ、増分を時間単位で保存
2. アップロード資産: S3 などオブジェクトストレージにコピーしバージョン管理
3. リストア手順: 手順書を明確化し、復元時間（RTO）とデータ損失許容度（RPO）を定義
4. 定期テスト: 月次でリストア検証を実施し、復元ログを保存

検証コマンド（例: Postgres）:

```bash
pg_dump -Fc -h db-host -U user app_db > dump_$(date +%F).dump
pg_restore -d restore_db dump_2026-04-01.dump
```

