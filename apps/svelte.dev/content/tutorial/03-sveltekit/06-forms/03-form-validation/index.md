---
title: Validation
---

ユーザーはいたずら好きな集団であり、隙あらばあらゆる種類の無意味なデータを送信しようとします。彼らが混乱を引き起こすのを防ぐには、フォームデータを検証することが重要です。

第一防衛ラインは、ブラウザに[組み込まれたフォームバリデーション(built-in form validation)](https://developer.mozilla.org/ja/docs/Learn/Forms/Form_validation#%E7%B5%84%E3%81%BF%E8%BE%BC%E3%81%BF%E3%83%95%E3%82%A9%E3%83%BC%E3%83%A0%E6%A4%9C%E8%A8%BC%E3%81%AE%E5%88%A9%E7%94%A8)で、これによって、例えば `<input>` を必須項目としてマークすることが簡単に行えます。

```svelte
/// file: src/routes/+page.svelte
<form method="POST" action="?/create">
	<label>
		add a todo
		<input
			name="description"
			autocomplete="off"
			+++required+++
		/>
	</label>
</form>
```

`<input>` を空にしたまま Enter を押してみてください。

この種類のバリデーションは役に立ちますが、十分ではありません。`<input>` の属性では表現できないバリデーションルール (例えば一意性) もありますし、いずれの場合においても、ユーザーがエリートハッカーなら、ブラウザのデベロッパーツールを使用して属性を削除してしまうかもしれません。このようないたずらから防御するには、常にサーバーサイドのバリデーションを使用する必要があります。

`src/lib/server/database.js` で、description が存在すること、そして一意であることをバリデートします。

```js
/// file: src/lib/server/database.js
export function createTodo(userid, description) {
+++	if (description === '') {
		throw new Error('todo must have a description');
	}+++

	const todos = db.get(userid);

+++	if (todos.find((todo) => todo.description === description)) {
		throw new Error('todos must be unique');
	}+++

	todos.push({
		id: crypto.randomUUID(),
		description,
		done: false
	});
}
```

重複した todo を送信してみてください。おっと！ SvelteKit は不親切なエラーページを表示していますね。サーバーでは 'todos must be unique' エラーを見ることができますが、予期せぬエラーメッセージには機密情報が含まれる可能性があるため、SvelteKit ではそれをユーザーには隠しています。

同じページを表示させたまま何が問題だったのかを示し、ユーザーがそれを修正できるようにするほうが良いでしょう。これを行うために、`fail` 関数を使用して、action からデータと適切な HTTP ステータスコードを返すことができます。

```js
/// file: src/routes/+page.server.js
+++import { fail } from '@sveltejs/kit';+++
import * as db from '$lib/server/database.js';

export function load({ cookies }) {...}

export const actions = {
	create: async ({ cookies, request }) => {
		const data = await request.formData();

+++		try {+++
			db.createTodo(cookies.get('userid'), data.get('description'));
+++		} catch (error) {
			return fail(422, {
				description: data.get('description'),
				error: error.message
			});
		}+++
	}
```

`src/routes/+page.svelte` では、`form` prop を介してその戻り値にアクセスすることができます。このプロパティはフォーム送信の後にのみ、値が入っています。

```svelte
/// file: src/routes/+page.svelte
<script>
	let { data, +++form+++ } = $props();
</script>

<div class="centered">
	<h1>todos</h1>

	+++{#if form?.error}
		<p class="error">{form.error}</p>
	{/if}+++

	<form method="POST" action="?/create">
		<label>
			add a todo:
			<input
				name="description"
				+++value={form?.description ?? ''}+++
				autocomplete="off"
				required
			/>
		</label>
	</form>
```

> [!NOTE] `fail` でラップしなくても、action から値を返すことができます。例えば、データが保存されたときに 'success!' というメッセージを返すこともできます。それも `form` prop を介してアクセスすることができます。
