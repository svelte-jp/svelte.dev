---
title: Component bindings
---

DOM 要素のプロパティにバインドできるのと同様に、コンポーネントの props にもバインドできます。例えば、フォーム要素のように `<Keypad>` コンポーネントの `value` prop にバインドすることができます。

まず、prop を _(バインド可能)bindable_ なものとしてマークする必要があります。`Keypad.svelte` の中で、`$props()` 宣言で `$bindable` Rune を使用するように更新します:

```js
/// file: Keypad.svelte
let { value +++= $bindable('')+++, onsubmit } = $props();
```

それから、`App.svelte` で `bind:` ディレクティブを追加します:

```svelte
/// file: App.svelte
<Keypad +++bind:value={pin}+++ {onsubmit} />
```

これで、ユーザがキーパッドを操作すると、親コンポーネントの `pin` の値が即座に更新されるようになりました。

> [!NOTE] コンポーネントバインディングは控えめに使用してください。それらが多すぎるとアプリケーションの周りのデータの流れを追跡するのが困難になります。特に「信頼できる唯一の情報源(single source of truth)」が存在しない場合には。
