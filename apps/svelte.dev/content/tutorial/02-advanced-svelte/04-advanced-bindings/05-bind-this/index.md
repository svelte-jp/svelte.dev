---
title: This
---

コンポーネントにある要素を読み取り専用のバインディングにするための特別なディレクティブとして、`bind:this` を使用することができます。

この演習の `$effect` では、canvas context を作成しようとしていますが、`canvas` は `undefined` です。まずコンポーネントのトップレベルで宣言することから始めましょう...

```svelte
/// file: App.svelte
<script>
	import { paint } from './gradient.js';

	+++let canvas;+++

	$effect(() => {
		// ...
	});
</script>
```

...それからディレクティブを `<canvas>` 要素に追加します:

```svelte
/// file: App.svelte
<canvas +++bind:this={canvas}+++ width={32} height={32}></canvas>
```

コンポーネントがマウントされるまで `canvas` は `undefined` のままであることにご注意ください。言い換えると、`$effect` が実行されるまでアクセスできないということです。
