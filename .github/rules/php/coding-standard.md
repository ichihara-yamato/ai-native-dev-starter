# PHP Coding Standard

## Purpose
- PHP 実装全般に適用する実装規約を定義する。
- PHPDoc の書き方は `.github/rules/php/phpdoc.md` を正本とする。
- Laravel 固有の責務分離は `.github/rules/laravel/architecture.md` を参照する。

## Formatting (PSR-12)
- インデントはスペース 4 つを使う。タブ禁止。
- 1 行の長さは 120 文字以内を目安とする。
- クラスの開き波括弧は次の行に置く。メソッドも同様。
- 制御構文（if / for / foreach / while）の開き波括弧は同じ行に置く。
- `else if` ではなく `elseif` を使う。

## Naming Conventions
- クラス名は PascalCase にする（例: `ArticleController`）。
- メソッド名・変数名は camelCase にする（例: `getUserName`）。
- 定数は UPPER_SNAKE_CASE にする（例: `MAX_RETRY_COUNT`）。
- プライベートプロパティに `_` プレフィックスを付けない。
- 省略名は一般的なもの（`id`, `url`, `api`）に限定する。

## Type Declarations
- 引数と戻り値には必ずネイティブ型を宣言する。
- null 許容は `?Type` または `Type|null` で明示し、理由のない nullable を避ける。
- `mixed` は型が本当に不定の場合に限定し、安易に使わない。
- 配列の要素型や連想配列の構造は PHPDoc で補足する。

## Class Design
- 1 クラス 1 責務を原則とし、複数の役割を持つクラスを作らない。
- 外部依存（DB、API、ファイルI/O）はインターフェースで抽象化し、コンストラクタで注入する。
- `static` メソッドは副作用のないユーティリティ処理に限定する。
- マジックメソッド（`__get`, `__set`, `__call`）の乱用を避ける。

## Error Handling
- 期待されない状態には例外を投げ、`false` や `null` の返却で握りつぶさない。
- 例外クラスは意味のある名前にし、基底の `\Exception` を直接 throw しない。
- catch した例外を再 throw する場合は元の例外を `$previous` に渡す。
- 呼び出し側が対処できない例外はログに記録してから伝播させる。

## Immutability And Side Effects
- 引数を内部で書き換えない。変換が必要なら新しい変数に代入する。
- メソッドの副作用（DB 書き込み、ファイル操作）は名前や PHPDoc で明示する。
- Value Object 相当のクラスはプロパティを `readonly` にする（PHP 8.1+）。

## Autoloading
- PSR-4 オートロードに従い、ファイルパスとクラス名を一致させる。
- 1 ファイルに複数のクラスを定義しない。
