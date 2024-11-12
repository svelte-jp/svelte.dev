---
title: handleFetch
---

`event` オブジェクトは標準の [Fetch API](https://developer.mozilla.org/ja/docs/Web/API/Fetch_API) のように振る舞う `fetch` メソッドを持っていますが、以下のスーパーパワーを備えています:

- 受け取ったリクエストから `cookie` と `authorization` を継承するので、サーバー上で認証付きのリクエストを行うことができます
- サーバー上で相対リクエストを行うことができます (通常、`fetch` をサーバーで使用する場合はオリジンを持つ URL が必要です)
- 内部リクエスト (例えば `+server.js` ルートに対するリクエスト) は、サーバー上で実行される場合は直接ハンドラ関数を呼び出すため、HTTP 呼び出しのオーバーヘッドがありません

この動作は `handleFetch` hook で変更することができます。デフォルトではこのようになります:

```js
/// file: src/hooks.server.js
export async function handleFetch({ event, request, fetch }) {
	return await fetch(request);
}
```

例えば、`src/routes/a/+server.js` に対するリクエストに対し、代わりに `src/routes/b/+server.js` のレスポンスを返すことができます:

```js
/// file: src/hooks.server.js
export async function handleFetch({ event, request, fetch }) {
+++	const url = new URL(request.url);
	if (url.pathname === '/a') {
		return await fetch('/b');
	}+++

	return await fetch(request);
}
```

後に、[universal `load` 関数](universal-load-functions)を学習するとき、`event.fetch` はブラウザでも呼び出せることを学びます。ブラウザからリクエストするときは `https://api.yourapp.com` のようなパブリックな URL で、それをサーバー上で実行するときは内部 URL にリダイレクトしたいとき (API サーバーとパブリックなインターネットの間にあるロードバランサーやプロキシーをバイパスしたいとき)、`handleFetch` はとても有用です。