---
title: Styling
---

HTMLと同じように、コンポーネントには`<style>`タグを置くことができます。`<p>`要素にいくつかスタイルを追加してみましょう。

```svelte
/// file: App.svelte
<p>This is a paragraph.</p>

<style>
+++	p {
		color: goldenrod;
		font-family: 'Comic Sans MS', cursive;
		font-size: 2em;
	}+++
</style>
```

重要なのは、これらのスタイルがこのコンポーネントにのみ適用されるということです。次のステップで説明しますが、アプリの別の箇所の`<p>`要素のスタイルに影響を与えてしまうようなことはありません。
