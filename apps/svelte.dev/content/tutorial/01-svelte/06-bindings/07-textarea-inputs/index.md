---
title: Textarea inputs
---

Svelteでは、`<textarea>` 要素は text input と同じように振る舞います。`bind:value`を使ってみましょう。

```svelte
/// file: App.svelte
<textarea +++bind:value=+++{value}></textarea>
```

このように名前が一致する場合は、省略形を使用することもできます。

```svelte
/// file: App.svelte
<textarea +++bind:value+++></textarea>
```

これは textarea に限らず全てのバインディングに適用されます。
