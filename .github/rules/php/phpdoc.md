# PHP PHPDoc Rules

## Purpose
- PHP のソースコードに付与する PHPDoc の記述ルールを共通化する。
- Laravel 以外の PHP フレームワークを追加した場合も再利用できるようにする。
- IDE、PhpStorm、PHPStan などの補助情報として一貫した型情報と説明を提供する。

## Basic Syntax
- PHPDoc は必ず `/**` で始め、各行の先頭に `*` を置き、`*/` で閉じる。
- 先頭には1行要約を書く。
- 必要な場合のみ空行を挟んで詳細説明を書く。
- 型情報はタグで記述し、説明文に混在させない。

## Required Targets
- クラスの直上にはクラス概要の PHPDoc を記述する。
- public/protected メソッドには PHPDoc を記述する。
- 型が読み取りづらいプロパティ、配列、コレクション、連想配列、複合型には PHPDoc を記述する。
- ローカル変数でも、ネイティブ型だけでは意図が伝わらない場合は `@var` を使う。

## Method Rules
- メソッドの PHPDoc には `@param`、`@return`、必要に応じて `@throws` を記述する。
- 要約では「何をするか」を1行で簡潔に書く。
- 例外を送出する可能性がある場合は、失敗経路を隠さず `@throws` に明示する。

## Common Tags
- `@param`: 引数の型、変数名、説明
- `@return`: 戻り値の型、説明
- `@var`: プロパティまたは変数の型
- `@throws`: 送出される可能性がある例外
- `@deprecated`: 非推奨のコード
- `@see`: 関連メソッド、関連 URL、参照先

## Type Policy
- PHP のネイティブ型宣言を優先し、PHPDoc の型情報と矛盾させない。
- ネイティブ型があっても、説明や補足が必要なら PHPDoc に記述する。
- 配列は `Type[]` または `array<KeyType, ValueType>` を使う。
- 複合型は `TypeA|TypeB` を使う。
- null 許容は `Type|null` を使う。
- PHPStan を考慮し、配列構造、要素型、コレクション要素型が重要な場合は PHPDoc で補足する。

## Writing Principles
- コードをそのまま言い換えるだけの文を書かない。
- シグネチャ、戻り値、例外、責務が変わった場合は PHPDoc も同時に更新する。
- 要約、タグ順、型表現はプロジェクト内で統一する。
- 不要な冗長説明は避けるが、利用者が誤解する省略はしない。

## Example
```php
/**
 * ユーザーIDからユーザー名を取得する
 *
 * @param int $userId ユーザーID
 * @return string ユーザー名
 * @throws \RuntimeException ユーザーが見つからない場合
 */
public function getUserName(int $userId): string
{
    // ...
}
```