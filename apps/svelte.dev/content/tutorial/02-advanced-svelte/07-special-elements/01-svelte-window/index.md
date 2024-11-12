---
title: <svelte:window>
---

イベントリスナーを任意の DOM 要素に追加できるのと同じように、`window` オブジェクトにも `<svelte:window>` でイベントリスナーを追加できます。

すでに `onkeydown` 関数を宣言しているので、あとはこれをつなげるだけです:

```svelte
/// file: App.svelte
<svelte:window +++{onkeydown}+++ />
```
