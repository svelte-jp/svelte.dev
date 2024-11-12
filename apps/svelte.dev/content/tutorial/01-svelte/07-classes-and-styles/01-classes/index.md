---
title: The class directive
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

ただ、もっと良くすることができます。何らかの条件に基づいてクラスを追加したり削除したりすることは UI 開発ではよくあるパターンで、Svelteにはこれを簡略化するための特別なディレクティブがあります:

```svelte
/// file: App.svelte
<button
	class="card"
	+++class:flipped={flipped}+++
	onclick={() => flipped = !flipped}
>
```

このディレクティブは、'`flipped` が truthy なときはいつでも `flipped` クラスを追加する' という意味です。
