---
title: Layouts
---

アプリの別々のルート(routes)が共通の UI を共有することがあると思います。その共通の UI を `+page.svelte` コンポーネントに繰り返し書く代わりに、同じディレクトリ内の全てのルート(routes)に適用される `+layout.svelte` コンポーネント を使用することができます。

このアプリには2つのルート(routes) `src/routes/+page.svelte` と `src/routes/about/+page.svelte` があり、どちらにも同じナビゲーション UI があります。新たに `src/routes/+layout.svelte` ファイルを作成してみましょう…

```
src/routes/
├ about/
│ └ +page.svelte
+++├ +layout.svelte+++
└ +page.svelte
```

…そして2つの `+page.svelte` ファイルで重複しているコンテンツを、新たに作成した `+layout.svelte` ファイルに移動しましょう。`{@render children()}` タグは、ページコンテンツがレンダリングされる場所です。

```svelte
/// file: src/routes/+layout.svelte
<script>
	let { children } = $props();
</script>

<nav>
	<a href="/">home</a>
	<a href="/about">about</a>
</nav>

{@render children()}
```

`+layout.svelte` ファイルは全ての子ルート(route)に適用されます。同じ階層にある `+page.svelte` にも適用されます(もし存在していれば)。レイアウトは任意の深さまでネストすることができます。
