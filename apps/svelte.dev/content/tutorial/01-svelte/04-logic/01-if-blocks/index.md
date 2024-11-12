---
title: If blocks
---

HTML には条件式やループのような _ロジック_ を表現する方法がありません。Svelteにはあります。

条件付きでマークアップをレンダリングする場合は、そのマークアップを `if` ブロックで囲みます。`count` が 10 より大きいときに表示されるテキストを追加してみましょう:

```svelte
/// file: App.svelte
<button onclick={increment}>
	Clicked {count}
	{count === 1 ? 'time' : 'times'}
</button>

+++{#if count > 10}
	<p>{count} is greater than 10</p>
{/if}+++
```

試してみてください。コンポーネントを更新し、ボタンを何回かクリックしてみてください。
