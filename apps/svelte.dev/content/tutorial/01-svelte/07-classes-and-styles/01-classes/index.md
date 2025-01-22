---
title: The class attribute
---

他の属性と同じように、JavaScriptの属性でクラスを指定することができます。ここでは、`flipped` クラスを card に追加します:

```svelte
/// file: App.svelte
<button
	class="card {+++flipped ? 'flipped' : ''+++}"
	onclick={() => flipped = !flipped}
>
```

これで期待通りに動作します — card をクリックすると、反転(flip)します。

ただ、もっと良くすることができます。何らかの条件に基づいてクラスを追加したり削除したりすることは UI 開発ではよくあるパターンで、Svelte では [clsx](https://github.com/lukeed/clsx) によって文字列に変換されたオブジェクトや配列を渡すことができます:

```svelte
/// file: App.svelte
<button
	+++class={["card", { flipped }]}+++
	onclick={() => flipped = !flipped}
>
```

これは、'`card` クラスは常に追加し、`flipped` が truthy なときは `flipped` クラスを追加する' という意味です。

条件付きのクラスを組み合わせる方法の詳細な例については、[`class` ドキュメントをご参照ください](/docs/svelte/class)。
