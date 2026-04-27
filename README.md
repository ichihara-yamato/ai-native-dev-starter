# ai-native-dev-starter

GitHub Copilot・Claude Code・OpenAI Codex CLI に対応した AI ネイティブ開発用の設定スターターです。

## 含まれるもの

| ディレクトリ / ファイル | 内容 |
|------------------------|------|
| `.github/copilot-instructions.md` | GitHub Copilot 共通指示 |
| `.github/CLAUDE.md` | Claude Code 自動ロード設定 |
| `AGENTS.md` | Codex CLI / Copilot Agent 自動ロード設定 |
| `.github/prompts/` | 役割別プロンプト（architect / engineer / reviewer 等） |
| `.github/rules/` | スタック別コーディングルール |
| `.claude/commands/` | Claude Code スラッシュコマンド（スキル） |

## 対応スタック

Laravel / PHP / Python / TypeScript (React・Vue 3) / Flutter / Rails

## 導入方法

自分のプロジェクトに使う場合は `.github/` と `.claude/` をコピーし、
`AGENTS.md` をプロジェクトルートに置いてください。

### バージョンについて

**`latest` ブランチが常に最新リリースを指しているため、`latest` の使用を推奨します。**

**初回取得（クローン）**

```bash
git clone -b latest --depth 1 https://github.com/ichihara-yamato/ai-native-dev-starter.git
```

**アップデート（取得済みの場合）**

```bash
git pull origin latest
```

特定バージョンを固定したい場合は `release/x.x.x` ブランチを指定してください。

```bash
git clone -b release/1.0.0 --depth 1 https://github.com/ichihara-yamato/ai-native-dev-starter.git
```

---

# エージェントへの指示ガイド

## 構成の考え方

この `.github/` は 2 層構造になっている。

```
① 自動ロード層  ─  CLAUDE.md / copilot-instructions.md / AGENTS.md
                    ツール起動時に自動で読み込まれ、ルール・構造・役割を注入する

② タスク層      ─  .github/prompts/ 配下のプロンプトファイル
                    作業種別に応じて呼び出し、具体的な指示を与える
```

指示の組み立て方：

```
指示 = 自動ロードされたルール（背景）+ 呼び出すプロンプト（役割・制約）+ タスク内容（今回の依頼）
```

---

## GitHub Copilot

### 自動ロード

| モード | 読み込まれるファイル |
|--------|-------------------|
| Chat / Inline | `copilot-instructions.md` |
| Agent モード | `copilot-instructions.md` + `AGENTS.md` |

---

### ① Chat: Run Prompt（推奨）

`mode: agent` frontmatter 付きのプロンプトファイルを直接実行できる。
**`#file:` と異なりプロンプトが「指示書」として確実に実行される。**

```
Ctrl / Cmd + Shift + P →「Chat: Run Prompt」→ 表示名で選択 → タスクを入力
```

選択できるプロンプトと表示名：

| 表示名 | ファイル | 用途 |
|--------|----------|------|
| PHP Implementation | `engineer/00-php-impl` | PHP 実装 |
| Laravel Implementation | `engineer/01-laravel-impl` | Laravel 実装 |
| Python Automation Implementation | `engineer/02-python-impl` | Python 実装 |
| TypeScript Implementation | `engineer/03-typescript-impl` | TypeScript 実装 |
| Flutter Implementation | `engineer/04-flutter-impl` | Flutter 実装 |
| Rails Implementation | `engineer/05-rails-impl` | Rails 実装 |
| Spec To Structure | `architect/01-spec-to-structure` | 要件 → 構造設計 |
| Code Review | `reviewer/01-code-review` | コードレビュー |
| Requirements To Spec | `designer/01-requirements-to-spec` | 要件 → 仕様書 |

---

### ② Chat モード — `#file:` でプロンプトを参照する

> **注意**: `#file:` はファイルを「参照」として添付する機能。
> 指示が曖昧だとプロンプトファイル自体が編集対象と誤認されることがある。
> **必ず「このファイルは指示書です」と明示すること。**

コピペ用テンプレート：

```
#file:.github/prompts/engineer/01-laravel-impl.prompt.md

↑このファイルは編集対象ではなく実行する指示書です。
この指示に従って、以下のタスクを実装してください。

【タスク】
（ここに作業内容を書く）
```

実例：

```
#file:.github/prompts/engineer/01-laravel-impl.prompt.md

↑このファイルは編集対象ではなく実行する指示書です。
この指示に従って、以下のタスクを実装してください。

【タスク】
ニュース記事の一覧・詳細・作成 API を実装してください。
エンドポイント: GET /api/v1/articles, POST /api/v1/articles
```

複数ファイルを参照する場合：

```
#file:.github/prompts/engineer/01-laravel-impl.prompt.md
#file:.github/structures/directory-map.md

↑1つ目のファイルは指示書、2つ目はプロジェクト構造の参考資料です。
この指示に従って、以下のタスクを実装してください。

【タスク】
（ここに作業内容を書く）
```

---

### ③ Agent モード — タスクを直接書く

`AGENTS.md` が自動ロードされるため、タスク内容だけで動く。
プロンプトファイルを意識する必要がない。

```
ニュース記事の CRUD API を Laravel で実装してください。
app/Actions パターンで、FormRequest のバリデーション付きで。
```

厳密に制御したいときだけ `#file:` を追加する（この場合も指示書であることを明示）：

```
#file:.github/prompts/engineer/laravel/03-action-pattern.prompt.md

↑このファイルは編集対象ではなく実行する指示書です。
この指示に従って、ArticleCreateAction を実装してください。
```

---

## Claude Code

### 自動ロード

`.github/CLAUDE.md` が起動時に自動で読み込まれる。

---

### ① スラッシュコマンド（推奨）

`.claude/commands/` にスキルが定義されているので、コマンド一行で呼び出せる。

```
/laravel ニュース記事の CRUD API を実装してください。
/review  PR の差分をレビューしてください。
/spec    ユーザー検索機能の要件から構造を設計してください。
```

| コマンド | 用途 |
|----------|------|
| `/laravel` | Laravel 実装 |
| `/php` | PHP 実装 |
| `/python` | Python 実装 |
| `/typescript` | TypeScript 実装 |
| `/flutter` | Flutter 実装 |
| `/rails` | Rails 実装 |
| `/spec` | 要件 → 構造設計 |
| `/api-design` | API 設計 |
| `/review` | コードレビュー |
| `/test-plan` | テスト計画 |
| `/security` | セキュリティチェック |
| `/ci` | CI パイプライン設定 |

---

### ② `@ファイルパス` で直接指定する場合

スキルにないプロンプトを使いたいときはファイルを直接参照する。
Claude Code では `@` で参照したファイルは**自動的に「指示書」として解釈される**ため、明示は不要。

```
@.github/prompts/engineer/laravel/03-action-pattern.prompt.md

ArticleCreateAction を実装してください。
```

---

### 実行フロー（三段構え）

Claude Code はコード出力前に作業計画を提示する。承認後に実行が始まる。

```
① 指示を出す
   /laravel ArticleCreateAction を実装してください。

      ↓

② エージェントが作業計画を提示
   Stack   : Laravel
   Role    : Engineer
   Rules   : rules/laravel/architecture.md, rules/php/phpdoc.md
   Actions : app/Actions/ArticleCreateAction.php を作成
             app/Http/Requests/ArticleRequest.php を作成

      ↓

③ 「OK」で実行開始
```

---

## OpenAI Codex CLI

### 自動ロード

`AGENTS.md` が起動時に自動で読み込まれる。

---

### タスクを直接書く（基本）

`AGENTS.md` がコンテキストを注入するため、タスク内容だけで動く。

```bash
codex "ニュース記事の CRUD API を Laravel で実装してください。"
```

---

### プロンプトファイルを指示書として渡す場合

```bash
codex "$(cat .github/prompts/engineer/01-laravel-impl.prompt.md)

---
タスク: ニュース記事の CRUD API を実装してください。"
```

---

## 共通リファレンス：シーン別早見表

| シーン | Copilot Chat: Run Prompt | Copilot `#file:`（参照） | Claude Code |
|--------|--------------------------|--------------------------|-------------|
| 要件 → 構造設計 | Spec To Structure | `architect/01-spec-to-structure` | `/spec` |
| Laravel 実装 | Laravel Implementation | `engineer/01-laravel-impl` | `/laravel` |
| PHP 実装 | PHP Implementation | `engineer/00-php-impl` | `/php` |
| TypeScript 実装 | TypeScript Implementation | `engineer/03-typescript-impl` | `/typescript` |
| Flutter 実装 | Flutter Implementation | `engineer/04-flutter-impl` | `/flutter` |
| Python 実装 | Python Automation Implementation | `engineer/02-python-impl` | `/python` |
| Rails 実装 | Rails Implementation | `engineer/05-rails-impl` | `/rails` |
| PR レビュー | Code Review | `reviewer/01-code-review` | `/review` |
| テスト計画 | — | `qa/01-feature-test-plan` | `/test-plan` |
| セキュリティ | — | `security/01-owasp-checklist` | `/security` |
| CI 設定 | — | `devops/01-ci-smoke` | `/ci` |
| API 設計 | — | `architect/01-api-design` | `/api-design` |

---

## Tips

- **タスクが大きい場合** は `/spec` または「Spec To Structure」で構造設計から始め、承認後に実装へ移る。
- **複数スタックにまたがる場合** は提供者側（API）と利用者側（frontend/mobile）の両方を書く。
- **既存コードを変更する場合** は対象ファイルも一緒に添付する。
- **制約が重要な作業** では禁止事項も明示する（「既存の hook 構成を崩さない」など）。

---

## 参照先

- コマンド定義一覧: `.github/task-format/command-list.md`
- ディレクトリ構造: `.github/structures/directory-map.md`
- ルール一覧: `.github/rules/`
