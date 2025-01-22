---
title: POST handlers
---

また、データを変更するハンドラを追加することもできます。例えば `POST` です。ただし、ほとんどのケースでは [form actions](the-form-element) を使うほうが良いでしょう — 書くコード量が少なくなり、JavaScript なしでも動作するので、よりレジリエンスになります。

'add a todo' `<input>` の `keydown` イベントハンドラの中で、データをサーバーに POST しましょう:

```svelte
/// file: src/routes/+page.svelte
<input
	type="text"
	autocomplete="off"
	onkeydown={async (e) => {
		if (e.key !== 'Enter') return;

		const input = e.currentTarget;
		const description = input.value;

+++		const response = await fetch('/todo', {
			method: 'POST',
			body: JSON.stringify({ description }),
			headers: {
				'Content-Type': 'application/json'
			}
		});+++

		input.value = '';
	}}
/>
```

ここでは、ユーザーの cookie にある `userid` を使用して `/todo` API ルート(route) に JSON を POST し、新たに作成した todo の `id` をレスポンスとして受け取っています。

`src/routes/todo/+server.js` ファイルを追加して、`src/lib/server/database.js` の `createTodo` を呼び出す `POST` ハンドラを記述し、`/todo` ルート(route)を作成しましょう。

```js
/// file: src/routes/todo/+server.js
import { json } from '@sveltejs/kit';
import * as database from '$lib/server/database.js';

export async function POST({ request, cookies }) {
	const { description } = await request.json();

	const userid = cookies.get('userid');
	const { id } = await database.createTodo({ userid, description });

	return json({ id }, { status: 201 });
}
```

`load` 関数や form actions と同様、`request` は標準の [Request](https://developer.mozilla.org/ja/docs/Web/API/Request) オブジェクトです; `await request.json()` はイベントハンドラから POST されたデータを返します。

データベースに新たに生成された todo の `id` をレスポンスとして [201 Created](https://http.dog/201) ステータスで返しています。イベントハンドラに戻り、これを使用してページを更新します:

```svelte
/// file: src/routes/+page.svelte
<input
	type="text"
	autocomplete="off"
	onkeydown={async (e) => {
		if (e.key !== 'Enter') return;

		const input = e.currentTarget;
		const description = input.value;

		const response = await fetch('/todo', {
			method: 'POST',
			body: JSON.stringify({ description }),
			headers: {
				'Content-Type': 'application/json'
			}
		});

+++		const { id } = await response.json();

		const todos = [...data.todos, {
			id,
			description
		}];

		data = { ...data, todos };+++

		input.value = '';
	}}
/>
```

> [!NOTE] ページをリロードしても同じ結果が取得できるような方法で `data` を変更する必要があります。`data` prop はリアクティブが深くない (not _deeply_ reactive) ので、置き換える必要があります — `data.todos = todos` のようなミューテーションでは再レンダリングが発生しません。
