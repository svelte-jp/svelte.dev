---
title: Animations
---

[前の章](/tutorial/svelte/deferred-transitions)では、要素が1つのToDoリストから別のリストに移動するときに、遷移の遅延を使用して動きの錯覚を作成しました。

この錯覚を完成させるには、遷移していない要素にもモーションを適用する必要があります。このために、`animate` ディレクティブを使用します。

最初に、`TodoList.svelte` に `flip` 関数（flip は ['First, Last, Invert, Play'](https://aerotwist.com/blog/flip-your-animations/) の略です）を `svelte/animate` からインポートします

```svelte
/// file: TodoList.svelte
<script>
	+++import { flip } from 'svelte/animate';+++
	import { send, receive } from './transition.js';

	let { todos, remove } = $props();
</script>
```

次に、それを `<li>` 要素に追加します:

```svelte
/// file: TodoList.svelte
<li
	class={{ done: todo.done }}
	in:receive={{ key: todo.id }}
	out:send={{ key: todo.id }}
	+++animate:flip+++
>
```

この場合、動きが少し遅いので、`duration` パラメータを追加することができます。

```svelte
/// file: TodoList.svelte
<li
	class={{ done: todo.done }}
	in:receive={{ key: todo.id }}
	out:send={{ key: todo.id }}
	animate:flip+++={{ duration: 200 }}+++
>
```

> [!NOTE] `duration` は `d => ミリ秒` 関数でもよいです。`d` は，要素が移動する必要があるピクセル数です。

すべてのトランジションとアニメーションが JavaScript ではなく CSS で適用されていて、メインスレッドをブロックすることはない（ブロックされることもない）という点に注意してください。
