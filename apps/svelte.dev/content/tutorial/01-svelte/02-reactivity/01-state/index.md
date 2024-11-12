---
title: State
---

Svelteの中心には、DOMを（例えば、イベントに応じて）アプリケーションの状態(state)に同期し続けさせるための強力な _リアクティビティ(reactivity)_ システムがあります。

`count` 宣言をリアクティブにするには、`$state(...)` で値をラップします。

```js
/// file: App.svelte
let count = +++$state(0)+++;
```

これは _Rune_ と呼ばれ、`count` が通常の変数ではないことを Svelte に伝えるためのものです。 Rune は関数のように見えますが、実際には違います — Svelte を使用する場合、これは言語の一部です。

あとは `increment` を実装するだけです:

```js
/// file: App.svelte
function increment() {
	+++count += 1;+++
}
```
