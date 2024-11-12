---
title: Select multiple
---

`<select>` 要素は `multiple` 属性を持つことができ、そうした場合は単一の値が選択されるのではなく、値が配列に入ります。

checkbox を `<select multiple>` で置き換えます:

```svelte
/// file: App.svelte
<h2>Flavours</h2>

+++<select multiple bind:value={flavours}>+++
	{#each ['cookies and cream', 'mint choc chip', 'raspberry ripple'] as flavour}
+++		<option>{flavour}</option>+++
	{/each}
+++</select>+++
```

`<option>` の `value` 属性はそのコンテンツと同じであるため、省略することができます。

> [!NOTE] `control` キー (MacOS の場合は `command` キー) を押したままにすると、複数の option を選択することができます。
