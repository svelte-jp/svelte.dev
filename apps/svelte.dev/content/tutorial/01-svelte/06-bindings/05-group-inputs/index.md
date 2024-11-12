---
title: Group inputs
---

同じ値に関連している `type="radio"` input や `type="checkbox"` input が複数ある場合、`value` 属性とともに `bind:group` を使うことができます。同じグループの radio input は互いに排他的(exclusive)です。同じグループの checkbox input は選択した値の配列を構成します。

`bind:group={scoops}` を radio input に追加し…

```svelte
/// file: App.svelte
<input
	type="radio"
	name="scoops"
	value={number}
	+++bind:group={scoops}+++
/>
```

…そして `bind:group={flavours}` を checkbox input に追加します:

```svelte
/// file: App.svelte
<input
	type="checkbox"
	name="flavours"
	value={flavour}
	+++bind:group={flavours}+++
/>
```
