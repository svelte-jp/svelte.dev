---
title: Custom dependencies
path: /Europe/London
---

`load` 関数の中で `fetch(url)` を呼ぶと、`url` を依存関係(dependency)として登録します。`fetch` を使用するのが適切でない場合もありますが、その場合は [`depends(url)`](/docs/kit/load#Rerunning-load-functions-Manual-invalidation) 関数を使って手動で依存関係を指定することができます。

`[a-z]+:` パターンで始まる文字列であれば有効な URL であるため、`data:now` のようなカスタムの invalidation key を作ることができます。

`src/routes/+layout.js` を更新します。`fetch` を呼び出すのではなく値を直接返すようにし、そして `depends` を追加します。

```js
/// file: src/routes/+layout.js
export async function load({ +++depends+++ }) {
	+++depends('data:now');+++

	return {
		now: +++Date.now()+++
	};
}
```

そして、`src/routes/[...timezone]/+page.svelte` にある `invalidate` 呼び出しも更新します。

```svelte
/// file: src/routes/[...timezone]/+page.svelte
<script>
	import { onMount } from 'svelte';
	import { invalidate } from '$app/navigation';

	let { data } = $props();

	onMount(() => {
		const interval = setInterval(() => {
			invalidate(+++'data:now'+++);
		}, 1000);

		return () => {
			clearInterval(interval);
		};
	});
</script>
```
