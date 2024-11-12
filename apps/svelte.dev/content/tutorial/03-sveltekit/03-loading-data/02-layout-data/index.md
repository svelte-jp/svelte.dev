---
title: Layout data
path: /blog
---

`+layout.svelte` ファイルが全ての子ルート(route)共通の UI を作るのと同じように、`+layout.server.js` ファイルは全ての子ルート(route)共通で使えるデータをロードします。

'more posts'(他の記事) サイドバーを、ブログ記事ページに追加したいと思います。`src/routes/blog/+page.server.js` で行っているのと同じように、`src/routes/blog/[slug]/+page.server.js` の `load` 関数から `summaries` を返すこともできますが、これでは同じことを繰り返すことになってしまいます。

代わりに、`src/routes/blog/+page.server.js` を `src/routes/blog/+layout.server.js` にリネームしましょう。`/blog` ルート(route)が動作し続けていることにご注目ください — `data.summaries` がまだページで利用できているのです。

では、記事ページ向けのレイアウトにサイドバーを追加しましょう:

```svelte
/// file: src/routes/blog/[slug]/+layout.svelte
<script>
	let { data, children } = $props();
</script>

<div class="layout">
	<main>
		{@render children()}
	</main>

+++	<aside>
		<h2>More posts</h2>
		<ul>
			{#each data.summaries as { slug, title }}
				<li>
					<a href="/blog/{slug}">{title}</a>
				</li>
			{/each}
		</ul>
	</aside>+++
</div>

<style>
	@media (min-width: 640px) {
		.layout {
			display: grid;
			gap: 2em;
			grid-template-columns: 1fr 16em;
		}
	}
</style>
```

レイアウト (とその下のページ) は、親の `+layout.server.js` から `data.summaries` を継承します。

ある記事から別の記事に移動したとき、記事自体のデータだけをロードするだけでよくなります — レイアウトのデータは有効なままです。もっと学習したければ、[invalidation](https://kit.svelte.jp/docs/load#rerunning-load-functions) のドキュメントをご覧ください。
