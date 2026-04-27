# Flutter State Management Rules

## Purpose
- provider または bloc を利用する際の状態管理方針を定義する。

## Responsibility Separation
- UI は状態を表示し、イベントを送ることに集中する。
- provider/bloc は状態遷移、ユースケース呼び出し、エラー反映を担当する。
- service は API 通信や外部 I/O を担当し、状態管理層と責務を分ける。

## State Design
- state は loading、data、error など利用者が判断できる形で表現する。
- 一時的 UI 状態と永続的な業務状態を混同しない。
- 同じ意味の状態を複数箇所で二重管理しない。

## Event Handling
- 画面イベントから直接 API を呼ばず、状態管理層を経由する。
- 初期表示、更新、再試行、入力変更などの契機を明確にする。
- 成功後に必要な再取得や画面遷移の条件を曖昧にしない。

## Testing Viewpoints
- 状態遷移の順序を確認する。
- 失敗時に UI が適切な状態を表示できることを確認する。
- 二重実行や連打時の挙動を確認する。
