# Python Automation Rules

## Purpose
- automation 配下の Python 実装ルールを定義する。

## Directory Responsibilities
- scripts は自動化処理のエントリーポイントを置く。
- models は Pydantic 等による入出力データ定義を置く。
- output は成果物保存先とし、コードやログを置かない。
- logs は Python 実行ログ専用とし、他層のログを混在させない。

## Implementation Principles
- 外部サイトや外部 API 呼び出しには timeout、retry、失敗時の扱いを持たせる。
- スクレイピング対象の DOM 依存は定数化または集約し、分散させない。
- 1スクリプトに取得、変換、保存、通知を密結合で詰め込みすぎない。
- 入出力データは dict のまま流さず、明示的なモデルへ変換する。

## Reliability
- 部分失敗時に何が完了し、何が未完了か分かるログを出す。
- 再実行時に重複保存や破損が起きない設計を優先する。
- エラーを握りつぶさず、必要な文脈を付けて記録する。

## Output Safety
- output に保存するファイル名、形式、保存先は予測可能にする。
- 個人情報、認証情報、機密値を output や logs にそのまま出さない。
- 生成物が後続処理で使われる場合は schema の整合を明確にする。
