# Laravel Architecture Rules

## Purpose
- Laravel 実装時の責務分離と配置ルールを定義する。
- Blade と Vite の asset 方針は `.github/rules/laravel/frontend-assets.md` を参照する。

## Layer Responsibilities
- Controllers はリクエスト受領、認可確認、Action 呼び出し、Response 返却に限定する。
- Actions は1ユースケース1クラスを原則とし、業務ロジックを集約する。
- Models は永続化、リレーション、スコープ、属性変換に責務を限定する。
- Resources はレスポンス整形のみを担当し、業務判断を入れない。
- routes/api.php では API エンドポイント定義に集中し、詳細ロジックを書かない。

## Request And Validation
- 入力検証は FormRequest などの専用手段に寄せる。
- Controller 内で配列を手作業で検証し続けない。
- バリデーションルールと DB 制約の意味が矛盾しないようにする。

## Action Design
- Action の入出力は明確にし、副作用を把握しやすい構造にする。
- 巨大な Action は private method や関連クラスへ分割する。
- 他 Action の多段ネストで流れを不透明にしない。

## PHPDoc Usage
- Laravel の PHPDoc 方針は `.github/rules/php/phpdoc.md` を正本として扱う。
- Laravel 実装では、Action、Controller、FormRequest、Resource、Model など追加・変更する PHP コードに対して共通 PHPDoc ルールを適用する。
- Eloquent の配列属性、Collection、スコープ、DTO 相当の配列構造など、Laravel 特有で型が曖昧になりやすい箇所は PHPDoc で補足する。

## Eloquent Usage
- N+1 を避けるため、必要に応じて eager loading を使う。
- fat controller は禁止し、fat model になりすぎる場合も専用クラスへ分離する。
- クエリ条件が再利用される場合は scope や query object 相当を検討する。

## API Consistency
- Resource の出力項目は frontend/mobile が利用する契約として扱う。
- エラー形式、HTTP ステータス、ページネーション形式は既存 API に合わせる。
- 仕様変更時は frontend/src/api と mobile/lib/services への影響を確認する。
