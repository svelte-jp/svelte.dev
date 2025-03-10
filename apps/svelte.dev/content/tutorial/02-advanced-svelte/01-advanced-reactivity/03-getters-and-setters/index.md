---
title: Getters and setters
---

クラスは、データを検証する必要がある場合に特に便利です。この `Box` クラスの場合、スライダーで許可されている最大値を超えて拡大し続けることはできないはずですが、実際には起ってしまっています。

これを修正するには、`width` と `height` を _getter_ と _setter_ (別名 _accessors_) に置き換えます。まず、これらを [プライベート プロパティ](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Classes/Private_properties) に変換します。

```js
/// file: App.svelte
class Box {
	+++#width+++ = $state(0);
	+++#height+++ = $state(0);
	area = $derived(this.+++#width+++ * this.+++#height+++);

	constructor(width, height) {
		this.+++#width+++ = width;
		this.+++#height+++ = height;
	}

	// ...
}
```

次に、いくつかのゲッターとセッターを作成します。

```js
/// file: App.svelte
class Box {
	// ...

+++	get width() {
		return this.#width;
	}

	get height() {
		return this.#height;
	}

	set width(value) {
		this.#width = value;
	}

	set height(value) {
		this.#height = value;
	}+++

	embiggen(amount) {
		this.width += amount;
		this.height += amount;
	}
}
```

最後に、セッターに検証を追加します。

```js
/// file: App.svelte
set width(value) {
	this.#width = +++Math.max(0, Math.min(MAX_SIZE, value));+++
}

set height(value) {
	this.#height = +++Math.max(0, Math.min(MAX_SIZE, value));+++
}
```

ボタンをどれだけ無理やり押しても、範囲入力の `bind:value` や `embiggen` メソッドを介して、ボックスのサイズを限度を超えて増やすことはできなくなりました。
