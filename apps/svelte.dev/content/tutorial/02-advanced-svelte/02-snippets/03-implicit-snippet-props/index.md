---
title: Implicit snippet props
---

利便性のため、コンポーネント内で直接宣言されたスニペットは、そのコンポーネントのプロパティになります。`header` および `row` スニペットを `<FilteredList>` 内に移動します。

```svelte
/// file: App.svelte
<FilteredList
	data={colors}
	field="name"
	{header}
	{row}
>
	+++{#snippet header()}...{/snippet}+++

	+++{#snippet row(d)}...{/snippet}+++
</FilteredList>

---{#snippet header()}...{/snippet}---

---{#snippet row(d)}...{/snippet}---
```

明示的なプロパティからこれらを削除できるようになりました。

```svelte
/// file: App.svelte
<FilteredList data={colors} field="name" ---{header} {row}--->
	{#snippet header()}...{/snippet}

	{#snippet row(d)}...{/snippet}
</FilteredList>
```

宣言されたスニペットの一部ではないコンポーネント内のコンテンツは、特別な `children` スニペットになります。`header` にはパラメーターがないため、ブロック タグを削除することで `children` に変えることができます...

```svelte
/// file: App.svelte
---{#snippet header()}---
<header>
	<span class="color"></span>
	<span class="name">name</span>
	<span class="hex">hex</span>
	<span class="rgb">rgb</span>
	<span class="hsl">hsl</span>
</header>
---{/snippet}---
```

...そして反対側で `header` プロパティの名前を `children` に変更します。

```svelte
/// file: FilteredList.svelte
<script>
	let { data, field, +++children+++, row } = $props();

	// ...
</script>
```

```svelte
/// file: FilteredList.svelte
<div class="header">
	+++{@render children()}+++
</div>
```
