---
title: navigating
---

`navigating` store は現在のナビゲーションを表しています。ナビゲーションを開始するとき — 例えばリンクをクリックしたり、ブラウザの '戻る/進む'、またはプログラムで `goto` を呼んだとき — `navigating` の値は以下のプロパティを持つオブジェクトになります:

- `from` と `to` — `params`、`route`、`url` プロパティを持つオブジェクト
- `type` — ナビゲーションのタイプ。例えば `link`、`popstate`、`goto`

> [!NOTE] タイプに関する全ての情報については [`Navigation`](https://kit.svelte.jp/docs/types#public-types-navigation) のドキュメントをご参照ください。

これは、長時間かかるナビゲーションのローディングインジケーターを表示するのに使用できます。この演習では、`src/routes/+page.server.js` と `src/routes/about/+page.server.js` の両方にわざと遅延を設けています。`src/routes/+layout.svelte` で、`navigating` store をインポートし、nav バーにメッセージを追加しましょう:

```svelte
/// file: src/routes/+layout.svelte
<script>
	import { page, +++navigating+++ } from '$app/stores';

	let { children } = $props();
</script>

<nav>
	<a href="/" aria-current={$page.url.pathname === '/'}>
		home
	</a>

	<a href="/about" aria-current={$page.url.pathname === '/about'}>
		about
	</a>

+++	{#if $navigating}
		navigating to {$navigating.to.url.pathname}
	{/if}+++
</nav>

{@render children()}
```
