---
title: Reactive built-ins
---

Svelte には、JavaScript 組み込みオブジェクトの代わりに使用できるいくつかのリアクティブ クラス (`Map`、`Set`、`Date`、`URL`、`URLSearchParams`) が付属しています。

この演習では、`$state(new Date())` を使用して `date` を宣言し、`setInterval` 内で再割り当てします。ただし、より適切な代替案は、[`svelte/reactivity`](/docs/svelte/svelte-reactivity) の `SvelteDate` を使用することです。

```svelte
/// file: App.svelte
<script>
	+++import { SvelteDate } from 'svelte/reactivity';+++

	let date = new +++SvelteDate();+++

	// ...
</script>
```
