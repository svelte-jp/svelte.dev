---
title: Invalidation
path: /Europe/London
---

ユーザーがあるページから別のページに移動するとき、SvelteKit はなにか変更があったと判断した場合にのみ `load` 関数を呼び出します。

この例では、タイムゾーン間の移動によって `src/routes/[...timezone]/+page.js` にある `load` 関数が再実行されます。`load` 関数の `params.timezone` が無効(invalid)になるからです。しかし、`src/routes/+layout.js` にある `load` 関数は再実行されません。なぜなら、SvelteKit から見れば、ナビゲーションでは何も変わらなかったからです。

[`invalidate(...)`](/docs/kit/$app-navigation#invalidate) 関数を使って、手動で無効化(invalidate)することでこれを修正できます。この関数は、URL を 引数に取り、それに依存している `load` 関数を再実行させます。`src/routes/+layout.js` にある `load` 関数は `fetch('/api/now')` を呼び出しているため、`/api/now` に依存しています。

`src/routes/[...timezone]/+page.svelte` に、1秒に1回 `invalidate('/api/now')` を呼び出す `onMount` コールバックを追加します。

```svelte
/// file: src/routes/[...timezone]/+page.svelte
<script>
	+++import { onMount } from 'svelte';+++
	+++import { invalidate } from '$app/navigation';+++

	let { data } = $props();

+++	onMount(() => {
		const interval = setInterval(() => {
			invalidate('/api/now');
		}, 1000);

		return () => {
			clearInterval(interval);
		};
	});+++
</script>

<h1>
	{new Intl.DateTimeFormat([], {
		timeStyle: 'full',
		timeZone: data.timezone
	}).format(new Date(data.now))}
</h1>
```

> [!NOTE] 特定の URL ではなくパターンに基づいて `invalidate` を実行したい場合、`invalidate` に関数を渡すこともできます。
