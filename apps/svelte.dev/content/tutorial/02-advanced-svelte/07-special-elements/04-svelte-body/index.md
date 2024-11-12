---
title: <svelte:body>
---

`<svelte:window>` や `<svelte:document>` と同様に、`<svelte:body>` 要素では `document.body` で発生するイベントをリッスンすることができます。これは `window` では発生しない `mouseenter` と `mouseleave` イベントを利用する際に便利です。

`<svelte:body>` タグに `onmouseenter` と `onmouseleave` ハンドラを追加してください…

```svelte
/// file: App.svelte
<svelte:body
	+++onmouseenter={() => hereKitty = true}+++
	+++onmouseleave={() => hereKitty = false}+++
/>
```

…そして、`<body>` の上をホバーしてみてください。
