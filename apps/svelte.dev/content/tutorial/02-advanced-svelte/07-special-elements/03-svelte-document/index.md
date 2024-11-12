---
title: <svelte:document>
---

`<svelte:document>` 要素では `document` で発生するイベントをリスンすることができます。これは、`selectionchange` のような、`window` では発生しないイベントを扱うときに便利です。

`onselectionchange` ハンドラを `<svelte:document>` タグに追加します:

```svelte
/// file: App.svelte
<svelte:document +++{onselectionchange}+++ />
```

> [!NOTE] `mouseenter` や `mouseleave` はすべてのブラウザで `document` では発生しないため、これらのハンドラをこの要素に追加しないでください。代わりに `<svelte:body>` を使用してください。
