---
title: Customizing use:enhance
---

`use:enhance` を使えば、ブラウザネイティブな動作をエミュレートするだけでなく、さらに踏み込んだことができます。コールバックを提供することで、**待機状態(pending states)** や **楽観的なUI(optimistic UI)** を追加することができます。私たちの2つの action にわざと遅延を追加し、遅いネットワークをシミュレートしましょう。

```js
/// file: src/routes/+page.server.js
export const actions = {
	create: async ({ cookies, request }) => {
		+++await new Promise((fulfil) => setTimeout(fulfil, 1000));+++
		...
	},

	delete: async ({ cookies, request }) => {
		+++await new Promise((fulfil) => setTimeout(fulfil, 1000));+++
		...
	}
};
```

アイテムを作成または削除するとき、UI の更新まで丸1秒かかるようになっており、ユーザーはなにか失敗したのかと思うようになります。これを解決するには、ローカルの状態(local state)をいくつか追加します…

```svelte
/// file: src/routes/+page.svelte
<script>
	import { fly, slide } from 'svelte/transition';
	import { enhance } from '$app/forms';

	let { data, form } = $props();

+++	let creating = $state(false);
	let deleting = $state([]);+++
</script>
```

…そして1つ目の `use:enhance` の内側で、`creating` を切り替えます。

```svelte
/// file: src/routes/+page.svelte
<form
	method="POST"
	action="?/create"
+++	use:enhance={() => {
		creating = true;

		return async ({ update }) => {
			await update();
			creating = false;
		};
	}}+++
>
	<label>
		add a todo:
		<input
			+++disabled={creating}+++
			name="description"
			value={form?.description ?? ''}
			autocomplete="off"
			required
		/>
	</label>
</form>
```

データを保存している間は、メッセージを表示することができます:

```svelte
/// file: src/routes/+page.svelte
<ul class="todos">
	<!-- ... -->
</ul>

+++{#if creating}
	<span class="saving">saving...</span>
{/if}+++
```

削除の場合、サーバーがなにか検証するのを待つ必要はありません — すぐに UI を更新することができます:

```svelte
/// file: src/routes/+page.svelte
<ul class="todos">
	{#each +++data.todos.filter((todo) => !deleting.includes(todo.id))+++ as todo (todo.id)}
		<li in:fly={{ y: 20 }} out:slide>
			<form
				method="POST"
				action="?/delete"
				+++use:enhance={() => {
					deleting = [...deleting, todo.id];
					return async ({ update }) => {
						await update();
						deleting = deleting.filter((id) => id !== todo.id);
					};
				}}+++
			>
				<input type="hidden" name="id" value={todo.id} />
				<button aria-label="Mark as complete">✔</button>

				{todo.description}
			</form>
		</li>
	{/each}
</ul>
```

> [!NOTE] `use:enhance` はとてもカスタマイズしやすく、フォーム送信の `cancel()`、リダイレクト処理、form をリセットするかどうかの制御、などを行うことができます。詳細については [ドキュメントをご覧ください](/docs/kit/$app-forms#enhance)。
