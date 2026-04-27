# Vue Patterns

## Component Design
- SFC は template、script、style の責務を明確に保つ。
- template に複雑な条件や計算を埋め込みすぎない。
- 画面固有のロジックが増えたら composable や子コンポーネントへ分割する。

## Script Setup
- props、emits、model は型付きで定義する。
- reactive と ref の使い分けを明確にし、曖昧な入れ子状態を避ける。
- computed で表現できる値を watch で無理に同期しない。

## Composables
- 再利用ロジックは composables に寄せ、UI 実装から分離する。
- composable は責務ごとに分け、巨大な万能 composable を作らない。
- API 通信を composable に置く場合も、型とエラー処理を明示する。

## Template Rules
- v-if と v-for の組み合わせで可読性が落ちる場合は分割する。
- イベント式に長い処理を直接書かない。
- 表示文言、状態判定、整形処理の責務を分離する。
