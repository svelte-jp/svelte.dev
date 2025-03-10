---
title: Spreading events
---

また、イベント ハンドラーを要素に直接 [_spread_](spread-props) することもできます。ここでは、`App.svelte` で `onclick` ハンドラーを定義しました。必要なのは、`BigRedButton.svelte` の `<button>` にプロパティを渡すだけです。

```svelte
/// file: BigRedButton.svelte
<button +++{...props}+++>
	Push
</button>
```
