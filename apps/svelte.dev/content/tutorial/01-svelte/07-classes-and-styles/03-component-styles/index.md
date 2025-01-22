---
title: Component styles
---

子コンポーネント内の style を指定したいことがよくあります。例えばこの演習では、このボックス(Box)を赤や緑、青にしたいです。

方法の1つとしては、`:global` CSS 修飾子を使います。これによって他のコンポーネントの中の要素を無差別にターゲットにすることができます:

```svelte
/// file: App.svelte
<style>
	.boxes :global(.box:nth-child(1)) {
		background-color: red;
	}

	.boxes :global(.box:nth-child(2)) {
		background-color: green;
	}

	.boxes :global(.box:nth-child(3)) {
		background-color: blue;
	}
</style>
```

しかし、こうすべきでない理由がたくさんあります。まず、とても冗長です。さらに、壊れやすいということです — `Box.svelte` の実装の詳細が変更されると、このセレクタが壊れるかもしれません。

なにより、無礼です。コンポーネントは、どの変数を props として公開するか決めるのと同じように、どの style を '外' から指定できるようにするか自身で決めることができるはずです。`:global` は最後の手段のエスケープハッチとして使用したほうがよいでしょうl．

`Box.svelte` の中で、`background-color` を変更し、[CSS カスタムプロパティ](https://developer.mozilla.org/ja/docs/Web/CSS/--*)で定義されるようにします:

```svelte
/// file: Box.svelte
<style>
	.box {
		width: 5em;
		height: 5em;
		border-radius: 0.5em;
		margin: 0 0 1em 0;
		background-color: +++var(--color, #ddd)+++;
	}
</style>
```

親要素 (例えば `<div class="boxes">`) であれば `--color` の値をセットできますが、コンポーネントごとにセットすることもできます:

```svelte
/// file: App.svelte
<div class="boxes">
	<Box +++--color="red"+++ />
	<Box +++--color="green"+++ />
	<Box +++--color="blue"+++ />
</div>
```

他の属性と同じようにこの値を動的にすることができます。

> [!NOTE] この機能は必要に応じてコンポーネントごとに `display: contents` がついた要素でラップし、カスタムプロパティを適用することによって実現しています。要素を確認すると、このようなマークアップになっているはずです:
>
> ```svelte
> <svelte-css-wrapper style="display: contents; --color: red;">
> 	<!-- contents -->
> </svelte-css-wrapper>
> ```
>
> `display: contents` のおかげでレイアウトには影響しませんが、追加された要素は `.parent > .child` のようなセレクタに影響します。
