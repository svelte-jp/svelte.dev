---
title: invalidateAll
path: /Europe/London
---

そして、最後の手段があります — `invalidateAll()` です。これは現在のページに関係する全ての `load` 関数を、何に依存しているかに関係なく全て再実行させます。

前回の演習から `src/routes/[...timezone]/+page.svelte` を更新します

```svelte
/// file: src/routes/[...timezone]/+page.svelte
<script>
	import { onMount } from 'svelte';
	import { +++invalidateAll+++ } from '$app/navigation';

	let { data } = $props();

	onMount(() => {
		const interval = setInterval(() => {
			+++invalidateAll();+++
		}, 1000);

		return () => {
			clearInterval(interval);
		};
	});
</script>
```

`src/routes/+layout.js` にある `depends` 呼び出しはもう必要ありません。

```js
/// file: src/routes/+layout.js
export async function load(---{ depends }---) {
	---depends('data:now');---

	return {
		now: Date.now()
	};
}
```

> [!NOTE] `invalidate(() => true)` と `invalidateAll` は同じではありません。`invalidateAll` は `url` の依存関係を持たない `load` 関数も再実行させますが、`invalidate(() => true)` はそうではありません。
