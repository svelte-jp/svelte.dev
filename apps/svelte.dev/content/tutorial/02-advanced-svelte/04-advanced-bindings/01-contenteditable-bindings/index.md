---
title: Contenteditable bindings
---

`contenteditable` 属性を持つ要素は、`textContent` と `innerHTML` のバインディングをサポートします。

```svelte
/// file: App.svelte
<div +++bind:innerHTML={html}+++ contenteditable />
```
