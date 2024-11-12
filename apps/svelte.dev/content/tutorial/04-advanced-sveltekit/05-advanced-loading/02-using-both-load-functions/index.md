---
title: Using both load functions
---

server load 関数と universal load 関数を一緒に使うことが必要なときもあるでしょう。例えば、サーバーからデータを返す必要がある一方で、サーバーのデータとしてシリアライズできない値も返す必要があるケースです。

この例では、`src/routes/+page.server.js` から返されるデータが `cool` かそうでないかに応じて、`load` から異なるコンポーネントを返したいと思います。

`src/routes/+page.js` で、`data` プロパティを使ってサーバーのデータにアクセスすることができます。

```js
/// file: src/routes/+page.js
export async function load(+++{ data }+++) {
	const module = +++data.cool+++
		? await import('./CoolComponent.svelte')
		: await import('./BoringComponent.svelte');

	return {
		component: module.default,
		message: +++data.message+++
	};
}
```

> [!NOTE] data がマージされていないことにご注意ください — 明示的に universal `load` 関数から `message` を返さなければなりません。
