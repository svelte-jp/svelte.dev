---
title: Checkbox inputs
---

チェックボックスは state を切り替えるのに使用されます。`input.value` にバインドする代わりに、`input.checked` にバインドします。

```svelte
/// file: App.svelte
<input type="checkbox" +++bind:+++checked={yes}>
```
