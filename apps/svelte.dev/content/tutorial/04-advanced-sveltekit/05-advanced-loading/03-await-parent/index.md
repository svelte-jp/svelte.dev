---
title: Using parent data
---

[layout data](/tutorial/kit/layout-data) のイントロダクションで見たように、`+page.svelte` コンポーネントと `+layout.svelte` コンポーネント は、親の `load` 関数から返された全てにアクセスすることができます。

時には、`load` 関数の中で親のデータにアクセスできると便利なことがあります。`await parent()` でこれを実現することができます。

どのように動作するかを示すため、異なる `load` 関数で取得した2つの数値を足してみましょう。まず、`src/routes/+layout.server.js` からデータを返します。

```js
/// file: src/routes/+layout.server.js
export function load() {
	return { +++a: 1+++ };
}
```

次に、`src/routes/sum/+layout.js` でそのデータを取得します。

```js
/// file: src/routes/sum/+layout.js
export async function load(+++{ parent }+++) {
	+++const { a } = await parent();+++
	return { +++b: a + 1+++ };
}
```

> [!NOTE] [universal](/tutorial/kit/universal-load-functions) `load` 関数は親の _server_ `load` 関数からデータを取得することができます。その逆は真ではありません。server load 関数は、別の server load 関数からのみ親のデータを取得することができます。

最後に、`src/routes/sum/+page.js` で、両方の `load` 関数から返される親のデータを取得しましょう。

```js
/// file: src/routes/sum/+page.js
export async function load(+++{ parent }+++) {
	+++const { a, b } = await parent();+++
	return { +++c: a + b+++ };
}
```

> [!NOTE] `await parent()` を使用する際はウォーターフォールを発生させないよう注意してください。親のデータに依存しない他のデータを取得(`fetch`)できるのであれば、そちらを先に行ってください。
