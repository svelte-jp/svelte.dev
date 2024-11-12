---
title: DOM events
---

今までざっと見てきたように、 要素の任意の DOM イベント (例えば click や [pointermove](https://developer.mozilla.org/ja/docs/Web/API/Element/pointermove_event)) をリスンするには、`on<name>` 関数を使用します:

```svelte
/// file: App.svelte
<div +++onpointermove={onpointermove}+++>
	The pointer is at {Math.round(m.x)} x {Math.round(m.y)}
</div>
```

他のプロパティと同様に、名前と値が一致する場合は短縮形を使用することができます:

```svelte
/// file: App.svelte
<div +++{onpointermove}+++>
	The pointer is at {Math.round(m.x)} x {Math.round(m.y)}
</div>
```
