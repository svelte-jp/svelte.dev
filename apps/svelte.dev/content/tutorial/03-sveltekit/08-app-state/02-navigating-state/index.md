---
title: navigating
---

`navigating`オブジェクトは、現在のナビゲーションを表します。リンクのクリック、戻る/進むナビゲーション、またはプログラムによる `goto` の呼び出しによってナビゲーションが開始されると、 `navigating` の値は以下のプロパティを持つオブジェクトになります。

- `from` と `to` — `params`、 `route` 、 `url` プロパティを持つオブジェクト
- `type` — ナビゲーションのタイプ。 例: `link`, `popstate` 、 `goto`

> [!NOTE] 型の完全な情報は、 [`Navigation`](/docs/kit/@sveltejs-kit#Navigation) ドキュメントにあります。

これは、時間のかかるナビゲーション中にローディングインジケーターを表示するために使えます。この演習では、 `src/routes/+page.server.js` と `src/routes/about/+page.server.js` にわざと遅延が設定されています。 `src/routes/+layout.svelte`に `navigating` オブジェクトをインポートし、ナビゲーションバーにメッセージを追加してください。

```svelte
/// file: src/routes/+layout.svelte
<script>
	import { page, +++navigating+++ } from '$app/state';

	let { children } = $props();
</script>

<nav>
	<a href="/" aria-current={page.url.pathname === '/'}>
		home
	</a>

	<a href="/about" aria-current={page.url.pathname === '/about'}>
		about
	</a>

+++	{#if navigating.to}
		navigating to {navigating.to.url.pathname}
	{/if}+++
</nav>

{@render children()}
```

> [!NOTE] SvelteKit 2.12より前は、`$app/stores` が提供する `$navigating` storeが同じ役割を担っていました。いま `$app/stores` を使っている場合は、 `$app/state` への移行をおすすめします。(Svelte 5が必要です。)