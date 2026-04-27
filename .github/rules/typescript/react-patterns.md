# React Patterns

## Component Design
- コンポーネントは表示責務を中心に保ち、データ取得や複雑な業務判断は hook 側へ寄せる。
- props は明示的に型付けし、必要最小限に絞る。
- 1コンポーネントが複数画面分の責務を持ち始めたら分割する。

## Hooks
- 再利用可能なロジックは custom hook に切り出す。
- hook は state、effect、イベント処理の関係が追える単位でまとめる。
- hook の戻り値は利用側が読んで意味が分かる名前にする。

## State Management
- 派生可能な値を不要に state 化しない。
- フォーム状態、API 状態、UI 表示状態を混同しない。
- 非同期処理では loading、success、error の状態を意識する。

## Effects And Events
- effect は外部同期のために使い、単なる計算処理には使わない。
- イベントハンドラ内の処理が膨らんだら関数へ抽出する。
- race condition や古いレスポンス反映に注意する。
