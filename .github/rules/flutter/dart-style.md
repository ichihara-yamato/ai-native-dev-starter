# Dart Style Rules

## Purpose
- Flutter/Dart 実装時の基本スタイルを定義する。

## File And Class Design
- 1ファイル1責務を原則とし、巨大な Widget ファイルを避ける。
- Widget、service、model、provider/bloc の責務を混在させない。
- 命名は役割が分かる具体名を使う。

## Widget Design
- build メソッドが長くなったら小さな Widget に分割する。
- UI の表示ロジックと業務ロジックを分離する。
- 非同期呼び出しを build 中に直接実行しない。

## Null Safety And Types
- null safety を前提に設計し、安易な nullable 多用を避ける。
- dynamic の使用は最小限にし、モデル型を明示する。
- API 応答や画面引数は型付きで扱う。

## Async And Error Handling
- service 呼び出しは成功時と失敗時の両方を設計する。
- 例外を握りつぶさず、UI へ必要な失敗状態を返す。
- 再読み込みや再試行が必要な画面では状態遷移を明示する。
