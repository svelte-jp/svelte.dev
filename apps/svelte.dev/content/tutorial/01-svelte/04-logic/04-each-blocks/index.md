---
title: Each blocks
---

ユーザーインターフェースを作る時、データのリストを扱うことがよくあります。この演習では、`<button>` マークアップを何度も繰り返し、その度に色を変えていますが、まだ追加するものがあります。

手間暇かけてコピー、ペースト、編集する代わりに、最初の button 以外を取り除き、そして `each` ブロックを使用します:

```svelte
/// file: App.svelte
<div>
	+++{#each colors as color}+++
		<button
			style="background: red"
			aria-label="red"
			aria-current={selected === 'red'}
			onclick={() => selected = 'red'}
		></button>
	+++{/each}+++
</div>
```

> [!NOTE] 式(この場合は `colors`)には、任意の iterable や配列に似たオブジェクトにすることができます。言い換えると、[`Array.from`](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/from) が使用できるならなんでも良いということです。

こうする場合、`"red"` の代わりに `color` 変数を使用する必要があります:

```svelte
/// file: App.svelte
<div>
	{#each colors as color}
		<button
			style="background: +++{color}+++"
			aria-label=+++{color}+++
			aria-current={selected === +++color+++}
			onclick={() => selected = +++color+++}
		></button>
	{/each}
</div>
```

第2引数として現在の _index_ をこのように取得することができます。

```svelte
/// file: App.svelte
<div>
	{#each colors as color, +++i}+++
		<button
			style="background: {color}"
			aria-label={color}
			aria-current={selected === color}
			onclick={() => selected = color}
		>+++{i + 1}+++</button>
	{/each}
</div>
```
