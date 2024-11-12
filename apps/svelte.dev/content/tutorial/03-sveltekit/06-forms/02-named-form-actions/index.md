---
title: Named form actions
---

単一の action しかないページというものは、実際にはかなりまれです。多くの場合、1つのページに複数の action を持たせる必要があるかと思います。このアプリでは、todo を作成するだけでは不十分で、一度完了した todo を削除したいと思います。

`default` action を、`create` と `delete` という名前を付けた action に置き換えるところから始めましょう。

```js
/// file: src/routes/+page.server.js
export const actions = {
	+++create+++: async ({ cookies, request }) => {
		const data = await request.formData();
		db.createTodo(cookies.get('userid'), data.get('description'));
	}+++,+++

+++	delete: async ({ cookies, request }) => {
		const data = await request.formData();
		db.deleteTodo(cookies.get('userid'), data.get('id'));
	}+++
};
```

> [!NOTE] default action と名前付きの action を共存させることはできません。

`<form>` 要素にはオプションの `action` 属性があり、これは `<a>` 要素にとっての `href` 属性と同じようなものです。新たに追加した `create` action を呼び出すようにするため、form を書き換えましょう。

```svelte
/// file: src/routes/+page.svelte
<form method="POST" +++action="?/create"+++>
	<label>
		add a todo:
		<input
			name="description"
			autocomplete="off"
		/>
	</label>
</form>
```

> [!NOTE] `action` 属性には任意の URL を指定することができます。別のページで定義されている action を呼び出したければ、`/todos?/create` のように指定することになるでしょう。ここでは action が _この_ ページにあるため、パス名を完全に省略することができるので、先頭が `?` 文字から始まっているのです。

次に、各 todo ごとに、一意な識別子を持つ hidden の `<input>` を含めた form を作りたいと思います。

```svelte
/// file: src/routes/+page.svelte
<ul class="todos">
	{#each data.todos as todo (todo.id)}
		<li>
+++			<form method="POST" action="?/delete">
				<input type="hidden" name="id" value={todo.id} />
				<span>{todo.description}</span>
				<button aria-label="Mark as complete"></button>
			</form>+++
		</li>
	{/each}
</ul>
```
