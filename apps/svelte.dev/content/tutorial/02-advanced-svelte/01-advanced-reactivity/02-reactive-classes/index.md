---
title: Reactive classes
---

リアクティブにできるのは変数だけではありません。Svelte では、クラスのプロパティもリアクティブにできます。

`Box` クラスの `width` プロパティと `height` プロパティをリアクティブにしてみましょう。

```js
/// file: App.svelte
class Box {
	width = +++$state(0);+++
	height = +++$state(0);+++
	area = 0;

	// ...
}
```

ここで、範囲入力を操作したり、「embiggen」ボタンをクリックすると、ボックスが反応します。

`$derived` を使用すると、`box.area` がリアクティブに更新されるようになります。

```js
/// file: App.svelte
class Box {
	width = $state(0);
	height = $state(0);
	area = +++$derived(this.width * this.height);+++

	// ...
}
```

> [!NOTE] `$state` と `$derived` に加えて、`$state.raw` と `$derived.by` を使用してリアクティブフィールドを定義することもできます。
