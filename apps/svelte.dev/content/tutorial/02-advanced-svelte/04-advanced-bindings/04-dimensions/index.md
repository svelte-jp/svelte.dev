---
title: Dimensions
---

任意の要素に `clientWidth`、 `clientHeight`、`offsetWidth`、`offsetHeight` バインディングを追加することができます。Svelte は、これらのバインドされた値を [`ResizeObserver`](https://developer.mozilla.org/ja/docs/Web/API/ResizeObserver) を使用して更新します:

```svelte
/// file: App.svelte
<div +++bind:clientWidth={w} bind:clientHeight={h}+++>
	<span style="font-size: {size}px" contenteditable>{text}</span>
	<span class="size">{w} x {h}px</span>
</div>
```

これらのバインディングは読み取り専用です。`w` と `h` の値を変更しても要素に何の影響もありません。

> [!NOTE] `display: inline` 要素は width や height を持ちません (`<img>` や `<canvas>` のような 'intrinsic' なディメンションを持つ要素は除く)、また `ResizeObserver` で監視することもできません。これらの要素の `display` スタイルを、`inline-block` などに変更する必要があります。
