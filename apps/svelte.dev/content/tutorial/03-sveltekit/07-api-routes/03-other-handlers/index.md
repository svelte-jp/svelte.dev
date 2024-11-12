---
title: Other handlers
---

同様に、他の HTTP verb のハンドラを追加できます。`src/routes/todo/[id]/+server.js` ファイルを作成し、`src/lib/server/database.js` の `toggleTodo` 関数と `deleteTodo` 関数を使用して todo の切り替えや削除を行う `PUT` と `DELETE` のハンドラを記述し、`/todo/[id]` ルート(route)を追加します:

```js
/// file: src/routes/todo/[id]/+server.js
import * as database from '$lib/server/database.js';

export async function PUT({ params, request, cookies }) {
	const { done } = await request.json();
	const userid = cookies.get('userid');

	await database.toggleTodo({ userid, id: params.id, done });
	return new Response(null, { status: 204 });
}

export async function DELETE({ params, cookies }) {
	const userid = cookies.get('userid');

	await database.deleteTodo({ userid, id: params.id });
	return new Response(null, { status: 204 });
}
```

ブラウザに実際のデータを返す必要はないため、空の [Response](https://developer.mozilla.org/ja/docs/Web/API/Response) を [204 No Content](https://http.dog/204) ステータスで返しています。

これで、イベントハンドラからこのエンドポイントを操作できるようになりました:

```svelte
/// file: src/routes/+page.svelte
<label>
	<input
		type="checkbox"
		checked={todo.done}
		onchange={async (e) => {
			const done = e.currentTarget.checked;

+++			await fetch(`/todo/${todo.id}`, {
				method: 'PUT',
				body: JSON.stringify({ done }),
				headers: {
					'Content-Type': 'application/json'
				}
			});+++
		}}
	/>
	<span>{todo.description}</span>
	<button
		aria-label="Mark as complete"
		onclick={async (e) => {
+++			await fetch(`/todo/${todo.id}`, {
				method: 'DELETE'
			});

			data.todos = data.todos.filter((t) => t !== todo);+++
		}}
	></button>
</label>
```
