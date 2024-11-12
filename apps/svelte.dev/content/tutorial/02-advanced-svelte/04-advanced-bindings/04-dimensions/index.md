---
title: Dimensions
---

全てのブロックレベル要素は `clientWidth`、 `clientHeight`、`offsetWidth`、`offsetHeight` バインディングを備えています:

```svelte
/// file: App.svelte
<div +++bind:clientWidth={w} bind:clientHeight={h}+++>
	<span style="font-size: {size}px" contenteditable>{text}</span>
	<span class="size">{w} x {h}px</span>
</div>
```

これらのバインディングは読み取り専用です。`w` と `h` の値を変更しても要素に何の影響もありません。
