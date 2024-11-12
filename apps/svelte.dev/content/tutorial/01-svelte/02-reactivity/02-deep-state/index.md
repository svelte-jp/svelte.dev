---
title: Deep state
---

前回の演習では state が _再代入_ に対してリアクティブになることを確認しましたが、それだけでなく、 _ミューテーション(mutations)_ に対してもリアクティブです — 私たちはこれを _ディープリアクティビティ(deep reactivity)_ と呼んでいます。

`numbers` をリアクティブな配列にしましょう:

```js
/// file: App.svelte
let numbers = +++$state([1, 2, 3, 4])+++;
```

こうすると、この配列を変更するときに...

```js
/// file: App.svelte
function addNumber() {
	+++numbers[numbers.length] = numbers.length + 1;+++
}
```

...コンポーネントが更新されます。また、代わりに配列に `push` することもできます:

```js
/// file: App.svelte
function addNumber() {
	+++numbers.push(numbers.length + 1);+++
}
```

> [!NOTE] Deep reactivity は [proxy](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Proxy) を使用して実装されており、proxy に対するミューテーションは元のオブジェクトには影響しません。
