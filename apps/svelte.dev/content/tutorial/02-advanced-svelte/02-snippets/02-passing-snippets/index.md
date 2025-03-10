---
title: Passing snippets to components
---

スニペットは関数と同様に単なる値なので、コンポーネントにプロパティとして渡すことができます。

この `<FilteredList>` コンポーネントを見てみましょう。このコンポーネントの役割は、渡される `data` をフィルタリングすることですが、そのデータをどのようにレンダリングするかについては何も関与しません。これは親コンポーネントの責任です。

すでにいくつかのスニペットが定義されています。まずはそれらを `<FilteredList>` に渡します。

```svelte
/// file: App.svelte
<FilteredList
	data={colors}
	field="name"
	+++{header}+++
	+++{row}+++
></FilteredList>
```

次に、反対側で、`header` と `row` をプロパティとして宣言します。

```svelte
/// file: FilteredList.svelte
<script>
	let { data, field, +++header, row+++ } = $props();

	// ...
</script>
```

最後に、プレースホルダーのコンテンツをレンダリング タグに置き換えます。

```svelte
/// file: FilteredList.svelte
<div class="header">
	+++{@render header()}+++
</div>

<div class="content">
	{#each filtered as d}
		+++{@render row(d)}+++
	{/each}
</div>
```

もう、`MistyRose` や `PeachPuff` の 16 進コードを記憶する必要はありません。
