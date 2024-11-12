---
title: setContext and getContext
---

context API は、データや関数を props として渡したり、たくさんのイベントをディスパッチしたりすることなく、コンポーネント同士で'会話'するための仕組みを提供します。これは高度ですが、便利な機能です。この演習では、generative art のパイオニアである George Nees の [Schotter](https://collections.vam.ac.uk/item/O221321/schotter-print-nees-georg/) を、context API を使って再現してみましょう。

`Canvas.svelte` にはアイテムを canvas に追加する `addItem` 関数があります。これを `<Canvas>` 内のコンポーネント (例えば `<Square>`) で利用できるようにするには、`setContext` を使います:

```js
/// file: Canvas.svelte
+++import { setContext } from 'svelte';+++
import { SvelteSet } from 'svelte/reactivity';

let { width = 100, height = 100, children } = $props();

let canvas;
let items = new SvelteSet();

+++setContext('canvas', { addItem });+++

function addItem(fn) {
	$effect(() => {
		items.add(fn);
		return () => items.delete(fn);
	});
}
```

子コンポーネントでは、この context を `getContext` で取得できます:

```js
/// file: Square.svelte
+++import { getContext } from 'svelte';+++

let { x, y, size, rotate } = $props();

+++getContext('canvas').addItem(draw);+++
```

ここまでは、そう…退屈ですよね。グリッドにランダム性を追加してみましょう:

```svelte
/// file: App.svelte
<div class="container">
	<Canvas width={800} height={1200}>
		{#each Array(12) as _, c}
			{#each Array(22) as _, r}
				<Square
					x={180 + c * 40+++ + jitter(r * 2)+++}
					y={180 + r * 40+++ + jitter(r * 2)+++}
					size={40}
					+++rotate={jitter(r * 0.05)}+++
				/>
			{/each}
		{/each}
	</Canvas>
</div>
```

`setContext` と `getContext` はコンポーネントの初期化中に呼び出す必要があります。これによって context が正しくバインドされます。このキー (この演習の場合は `'canvas'`) には文字列以外も含め、好きなものを指定でき、誰が context にアクセスできるのかコントロールするのに有用です。

> [!NOTE] context オブジェクトには、リアクティブな state を含めあらゆるものを含めることができます。これにより、時間の経過とともに変化する値を子コンポーネントに渡すことができます:
>
> ```js
> // in a parent component
> import { setContext } from 'svelte';
>
> let context = $state({...});
> setContext('my-context', context);
> ```
>
> ```js
> // in a child component
> import { getContext } from 'svelte';
>
> const context = getContext('my-context');
> ```
