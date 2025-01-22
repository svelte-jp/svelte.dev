---
title: Deferred transitions
---

Svelte のトランジションエンジンで特に強力な特徴は、トランジションを _遅延_ させて複数の要素間でトランジションが調整されるように出来ることです。

このペアのToDoリストを見てみましょう。ToDoを切り替えると反対側のリストに送られます。現実の世界ではオブジェクトはこのような振る舞いをしません。消えたり別の場所に現れたりするのではなく、一連の中間的な位置を移動します。モーションを使用することでアプリで何が起こっているのかをユーザーに理解してもらうことができます。

この効果は、`transition.js` にあるように、`send` と `receive` というトランジションのペアを作成する`crossfade` 関数を使用することで実現できます。要素は、「send」されると、対応する「receive」される要素を探し、その要素を相手の位置に変換してフェードアウトするトランジションを生成します。要素が「receive」されると、逆のことが起こります。対応する要素がない場合は、`fallback` トランジションが使われます。

`TodoList.svelte` を開いてください。まず、transition.js から `send` と `receive` をインポートしてください。

```svelte
/// file: TodoList.svelte
<script>
	+++import { send, receive } from './transition.js';+++

	let { todos, remove } = $props();
</script>
```

それから、`<li>` 要素にもそれらを追加し、`todo.id` プロパティを、要素にマッチするキーとして使用します。

```svelte
/// file: TodoList.svelte
<li
	class={{ done: todo.done }}
	+++in:receive={{ key: todo.id }}+++
	+++out:send={{ key: todo.id }}+++
>
```

これでアイテムを切り替えると、アイテムはスムーズに新しい場所に移動します。遷移していない項目は、まだ不器用に跳ね回っています。これは次の章で解決できます。
