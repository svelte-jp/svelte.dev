---
title: Derived state
---

しばしば、他の state から導出(derive)した state が必要になることがあるでしょう。このために、`$derived` Rune があります:

```js
/// file: App.svelte
let numbers = $state([1, 2, 3, 4]);
+++let total = $derived(numbers.reduce((t, n) => t + n, 0));+++
```

これをマークアップで使用できます:

```svelte
/// file: App.svelte
<p>{numbers.join(' + ')} = +++{total}+++</p>
```

`$derived` 宣言の中の式は、それが依存するもの (この演習では `numbers`) が更新されるたびに再評価されます。通常の state とは違い、derived state は読み取り専用です。
