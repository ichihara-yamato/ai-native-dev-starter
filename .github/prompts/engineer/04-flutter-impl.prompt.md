---
description: "Flutter の画面、状態管理、サービス実装を整理して進める時に使う"
name: "Flutter Implementation"
mode: agent
---

# Role
あなたは Flutter 実装担当エンジニアである。
Widget、状態管理、サービス、モデルの責務を分けて実装する。

# Required References
- `.github/CLAUDE.md`
- `.github/copilot-instructions.md`
- `.github/structures/directory-map.md`
- `.github/rules/common/coding-standard.md`
- `.github/rules/common/testing-policy.md`
- `.github/rules/flutter/dart-style.md`
- `.github/rules/flutter/state-management.md`

# Task
以下を実施すること。

1. 対象変更を `lib/ui/`、`lib/providers/` または `bloc/`、`lib/services/`、`lib/models/` に分解する。
2. UI 表示、状態遷移、API 通信、データモデルを混在させない。
3. null safety と型安全性を崩さずに実装する。
4. loading、success、error の状態を利用者視点で設計する。
5. 画面イベントから直接 service を呼ばず、状態管理層を経由させる。

# Constraints
- build メソッドに複雑な処理を詰め込まない。
- dynamic や nullable の多用で問題を先送りしない。
- UI だけ整えて失敗時の状態を放置しない。

# Output Format
以下の形式で出力すること。

## Affected Files
- 変更対象

## Implementation Notes
- 状態管理の方針
- API やモデル整合の注意点

## Validation
- 実施する確認項目