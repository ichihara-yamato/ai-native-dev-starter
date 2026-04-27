# Engineer: Laravel FormRequest

Role: Engineer
Purpose: Produce `FormRequest` validation stubs based on input specs.
Inputs: Field list, types, custom rules, auth context.
Constraints: Use validation rule arrays; move messages to resources where needed.
Outputs: `FormRequest` class with rules and authorization logic.

詳細テンプレート（使い方）:

- 入力フォーマット:
  - `name: string|required|max:255`
  - `age: integer|nullable|min:0`
  - `tags: array|nullable` といった形でフィールド定義を渡す。

- 生成される `FormRequest` の構成:
  - `authorize()` : 認可ロジック（例: `return $this->user()->can('update', $model);`）
  - `rules()` : 配列形式のバリデーションルール（`['title' => ['required','string','max:255']]`）
  - `messages()`（任意）: カスタムメッセージは`lang` ファイルへ外だし推奨。

例（生成されるコードの抜粋）:

```php
namespace App\Http\Requests;

use Illuminate\Foundation\Http\FormRequest;

class StoreNewsRequest extends FormRequest
{
	public function authorize(): bool
	{
		return $this->user() !== null; // 認証済みのみ許可
	}

	public function rules(): array
	{
		return [
			'title' => ['required', 'string', 'max:255'],
			'excerpt' => ['nullable', 'string', 'max:500'],
			'body' => ['required', 'string'],
			'published_at' => ['nullable', 'date'],
		];
	}

	public function messages(): array
	{
		return [
			'title.required' => __('validation.required', ['attribute' => 'title']),
		];
	}
}
```

ヒント:
- `Rule::unique(...)` や `Rule::in(...)` は配列で組み合わせる。
- API用は `FormRequest` を `Api\Requests` 下に置き、レスポンスは `422` として扱うルールを統一。
- ファイルアップロードや配列バリデーション（例: `images.*`）はサンプルを参照して追加。

