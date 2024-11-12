---
title: Adding parameters
---

トランジションとアニメーションと同じように、action は引数を取ることができます。その引数と、action 関数自身が属する要素を以って、action 関数は呼び出されます。

この演習では、[`Tippy.js`](https://atomiks.github.io/tippyjs/) ライブラリを使って `<button>` にツールチップを追加したいと思います。action はすでに `use:tooltip` によって紐付けられていますが、ボタンをホバーしても (キーボードでフォーカスしても) ツールチップには何も表示されません。

最初に、action でオプションを受け取り、それを Tippy に渡さなければなりません:

```js
/// file: App.svelte
function tooltip(node, +++fn+++) {
	$effect(() => {
		const tooltip = tippy(node, +++fn()+++);

		return tooltip.destroy;
	});
}
```

> [!NOTE] オプションそのものではなく関数を渡していますが、これは、`tooltip` 関数はオプションが変更されたときに再実行しないからです。

それから、オプションを action に渡します:

```svelte
/// file: App.svelte
<button use:tooltip+++={() => ({ content })}+++>
	Hover me
</button>
```

> [!NOTE] Svelte 4 では、action は `update` メソッドと `destroy` メソッドをもったオブジェクトを返していました。これはまだ動作しますが、代わりに `$effect` を使用することをおすすめします。そのほうがより柔軟できめ細やかだからです。
