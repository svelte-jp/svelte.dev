---
NOTE: do not edit this file, it is generated in apps/svelte.dev/scripts/sync-docs/index.ts
title: $state
---

`$state` rune を使用すると _リアクティブな state_ を作成することができます。その state を変更すると、UI に反映されるということです。

```svelte
<script>
	let count = $state(0);
</script>

<button onclick={() => count++}>
	clicks: {count}
</button>
```

(もしかしたらあなたが使用したことがあるかもしれない) 他のフレームワークとは違い、state を操作するための API はありません — `count` はオブジェクトや関数ではなくただの number であり、他の変数を更新するのと同じように更新することができます。

### Deep state

もし `$state` を配列やシンプルなオブジェクトで使用した場合、リアクティブが深い (原文: deeply reactive) _state proxy_ になります。[proxy](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Proxy) によって Svelte はプロパティが読み書き (`array.push(...)` のようなメソッド経由で行われたものを含む) されたときにコードを実行でき、きめ細やかな更新 (原文: granular updates) をトリガーすることができます。

state は、Svelte が配列やシンプルなオブジェクト(classなど)以外のものを見つけるまで再帰的に proxy 化 されます。このような場合...

```js
let todos = $state([
	{
		done: false,
		text: 'add more todos'
	}
]);
```

...個々の todo のプロパティが変更されると、UI の中の、その変更されたプロパティに依存する部分に対して更新がトリガーされます:

```js
let todos = [{ done: false, text: 'add more todos' }];
// ---cut---
todos[0].done = !todos[0].done;
```

配列に新たなオブジェクトを push すると、それも proxy 化されます。

```js
let todos = [{ done: false, text: 'add more todos' }];
// ---cut---
todos.push({
	done: false,
	text: 'eat lunch'
});
```

> [!NOTE] proxy のプロパティを更新しても、元のオブジェクトは変更されません。

もしリアクティブな値を分割した場合、その参照はリアクティブではありません — 通常の JavaScript と同じように、分割時点で評価されます:

```js
let todos = [{ done: false, text: 'add more todos' }];
// ---cut---
let { done, text } = todos[0];

// this will not affect the value of `done`
todos[0].done = !todos[0].done;
```

### Classes

class インスタンスは proxy されません。その代わりに、class のフィールド (public か private かを問わず) にも `$state` を使用するか、または `constructor` の内側で最初に代入するときに `$state` を使用することができます:

```js
// @errors: 7006 2554
class Todo {
	done = $state(false);

	constructor(text) {
		this.text = $state(text);
	}

	reset() {
		this.text = '';
		this.done = false;
	}
}
```

> [!NOTE] コンパイラは `done` と `text` を、プライベートなフィールドを参照する class prototype の `get`/`set` メソッドに変換します。これは、プロパティが enumerable ではないことを意味します。

JavaScript でメソッドを呼び出すとき、[`this`](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators/this) の値が問題になります。以下のコードは動作しません、なぜなら `reset` メソッドの中にある `this` が `Todo` ではなく `<button>` になるからです:

```svelte
<button onclick={todo.reset}>
	reset
</button>
```

インライン関数を使うこともできますし...

```svelte
<button onclick=+++{() => todo.reset()}>+++
	reset
</button>
```

...class の定義でアロー関数を使うこともできます:

```js
// @errors: 7006 2554
class Todo {
	done = $state(false);

	constructor(text) {
		this.text = $state(text);
	}

	+++reset = () => {+++
		this.text = '';
		this.done = false;
	}
}
```

> Svelte provides reactive implementations of built-in classes like `Set` and `Map` that can be imported from [`svelte/reactivity`](svelte-reactivity).

## `$state.raw`

オブジェクトや配列を、深いリアクティブ (deeply reactive) にしたくない場合は、`$state.raw` を使用します。

`$state.raw` で宣言された state は変更できません、再代入のみ可能です。言い換えると、もし更新したいのであれば、オブジェクトのプロパティに代入したり配列のメソッドの `push` などを使用するのではなく、オブジェクトや配列を丸ごと置き換えてください。

```js
let person = $state.raw({
	name: 'Heraclitus',
	age: 49
});

// this will have no effect
person.age += 1;

// this will work, because we're creating a new person
person = {
	name: 'Heraclitus',
	age: 50
};
```

変更する予定がない大きい配列やオブジェクトでこれを使用すると、パフォーマンスを改善することができます。リアクティブにするためのコストを避けられるからです。raw state には、リアクティブな state を含められることにご注意ください (例えば、リアクティブなオブジェクトの配列 (原文: a raw array of reactive objects))。

As with `$state`, you can declare class fields using `$state.raw`.

## `$state.snapshot`

深いリアクティブ (deeply reactive) な `$state` proxy の静的なスナップショットを取得するには、`$state.snapshot` を使用します:

```svelte
<script>
	let counter = $state({ count: 0 });

	function onclick() {
		// Will log `{ count: ... }` rather than `Proxy { ... }`
		console.log($state.snapshot(counter));
	}
</script>
```

これは、例えば `structuredClone` のような proxy を受け付けない外部のライブラリや API に state を渡したいときに便利です。

## 関数に state を渡す <!--Passing-state-into-functions-->

JavaScript は _値渡し_ の言語です — 関数を呼び出すとき、その引数は _変数_ ではなく _値_ です。言い換えると:

```js
/// file: index.js
// @filename: index.js
// ---cut---
/**
 * @param {number} a
 * @param {number} b
 */
function add(a, b) {
	return a + b;
}

let a = 1;
let b = 2;
let total = add(a, b);
console.log(total); // 3

a = 3;
b = 4;
console.log(total); // still 3!
```

もし `add` が `a` と `b` の現在の値にアクセスし、`total` の現在の値を返したいのであれば、代わりに関数を使う必要があります:

```js
/// file: index.js
// @filename: index.js
// ---cut---
/**
 * @param {() => number} getA
 * @param {() => number} getB
 */
function add(+++getA, getB+++) {
	return +++() => getA() + getB()+++;
}

let a = 1;
let b = 2;
let total = add+++(() => a, () => b)+++;
console.log(+++total()+++); // 3

a = 3;
b = 4;
console.log(+++total()+++); // 7
```

Svelte の state も同様です — `$state` rune で宣言されたものを参照するとき...

```js
let a = +++$state(1)+++;
let b = +++$state(2)+++;
```

...その現在の値にアクセスします。

'関数(function)' は意味が広範囲にわたることにご注意ください — proxy のプロパティや [`get`](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Functions/get)/[`set`](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Functions/set) プロパティも包含しています...

```js
/// file: index.js
// @filename: index.js
// ---cut---
/**
 * @param {{ a: number, b: number }} input
 */
function add(input) {
	return {
		get value() {
			return input.a + input.b;
		}
	};
}

let input = $state({ a: 1, b: 2 });
let total = add(input);
console.log(total.value); // 3

input.a = 3;
input.b = 4;
console.log(total.value); // 7
```

...もしこのようなコードを書いている場合は、代わりに [class](#Classes) を使用することをご検討ください。

## モジュール間で state を渡す <!--Passing-state-across-modules-->

`.svelte.js` や `.svelte.ts` ファイルでは state を宣言できますが、その state は直接再代入されていない場合に限り、エクスポートすることができます。言い換えると、以下のようなことはできないということです:

```js
/// file: state.svelte.js
export let count = $state(0);

export function increment() {
	count += 1;
}
```

その理由は、`count` に対するすべての参照は Svelte コンパイラによって変換されるからです — 上記のコードは大雑把に言えば以下と同じです:

```js
/// file: state.svelte.js (compiler output)
// @filename: index.ts
interface Signal<T> {
	value: T;
}

interface Svelte {
	state<T>(value?: T): Signal<T>;
	get<T>(source: Signal<T>): T;
	set<T>(source: Signal<T>, value: T): void;
}
declare const $: Svelte;
// ---cut---
export let count = $.state(0);

export function increment() {
	$.set(count, $.get(count) + 1);
}
```

> [!NOTE] Svelte が生成するコードは [playground](/playground) で 'JS Output' タブをクリックすると見ることができます。

Svelte のコンパイラは一度に1つのファイルのみ処理するため、もし別のファイルが `count` をインポートしている場合、Svelte はそれぞれの参照を `$.get` や `$.set` でラップする必要があるかどうかがわかりません:

```js
// @filename: state.svelte.js
export let count = 0;

// @filename: index.js
// ---cut---
import { count } from './state.svelte.js';

console.log(typeof count); // 'object', not 'number'
```

そのため、モジュール間で state を共有するには、2つの方法があります。1つ目は再代入をしないことです...

```js
// This is allowed — since we're updating
// `counter.count` rather than `counter`,
// Svelte doesn't wrap it in `$.state`
export const counter = $state({
	count: 0
});

export function increment() {
	counter.count += 1;
}
```

...2つ目は、直接エクスポートしないことです:

```js
let count = $state(0);

export function getCount() {
	return count;
}

export function increment() {
	count += 1;
}
```
