---
title: Reloading the page
---

通常、SvelteKit ではページをリフレッシュすることなくページ間を移動できます。この演習では、`/` と `/about` の間を移動してもタイマーが動き続けますが、これは移動のときにリフレッシュしていないからです。

まれに、この動作を無効にしたいときがあります。`data-sveltekit-reload` 属性を個々のリンクやリンクを含む要素に付けると、これを実現できます:

```svelte
/// file: src/routes/+layout.svelte
<nav +++data-sveltekit-reload+++>
	<a href="/">home</a>
	<a href="/about">about</a>
</nav>
```

link options とその値に関する詳細な情報については、[link options のドキュメント](https://kit.svelte.jp/docs/link-options)をご参照ください。