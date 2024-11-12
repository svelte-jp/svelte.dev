---
title: Select bindings
---

`<select>` 要素にも `bind:value` を使用できます。

```svelte
/// file: App.svelte
<select
    +++bind:+++value={selected}
    onchange={() => answer = ''}
>
```

`<option>` の値は文字列ではなくオブジェクトであることにご注意ください。Svelteは気にしません。

> [!NOTE] `selected` の初期値を設定していないので、バインディングは自動的にデフォルト値(配列の先頭)に設定されます。しかし、注意してください。バインディングが初期化されるまで、`selected` は undefined のままなので、よく考えもせずにテンプレート内の `selected.id` などを参照することはできません。
