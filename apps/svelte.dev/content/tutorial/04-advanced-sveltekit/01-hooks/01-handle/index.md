---
title: handle
---

SvelteKit では、フレームワークのデフォルトの振る舞いをインターセプトしてオーバーライドするための方法として、 _hooks_ をいくつか提供しています。

最も基本的な hook は `handle` で、`src/hooks.server.js` に置きます。`event` オブジェクトと `resolve` 関数を受け取り、[`Response`](https://developer.mozilla.org/ja/docs/Web/API/Response) オブジェクトを返します。

`resolve` は魔法が起きる場所です: SvelteKit は受け取ったリクエストの URL とアプリのルート(route)をマッチさせ、関連するコード (`+page.server.js` や `+page.svelte` ファイルなど) をインポートし、ルートに必要なデータを読み込み、レスポンスを生成します。

デフォルトの `handle` hook は以下のようなものです:

```js
/// file: src/hooks.server.js
export async function handle({ event, resolve }) {
	return await resolve(event);
}
```

ページについては ([API routes](get-handlers) とは対照的に)、生成された HTML を`transformPageChunk`で変更できます:

```js
/// file: src/hooks.server.js
export async function handle({ event, resolve }) {
	return await resolve(event, {
+++		transformPageChunk: ({ html }) => html.replace(
			'<body',
			'<body style="color: hotpink"'
		)+++
	});
}
```

また、まったく新しいルート(route)を作成することもできます:

```js
/// file: src/hooks.server.js
export async function handle({ event, resolve }) {
+++	if (event.url.pathname === '/ping') {
		return new Response('pong');
	}+++

	return await resolve(event, {
		transformPageChunk: ({ html }) => html.replace(
			'<body',
			'<body style="color: hotpink"'
		)
	});
}
```
