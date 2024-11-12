---
title: The RequestEvent object
---

`handle` に渡される `event` オブジェクトは、`+server.js` ファイルの [API routes](get-handlers) や `+page.server.js` ファイルの [form actions](the-form-element) や `+page.server.js` と `+layout.server.js` の `load` 関数に渡されるものと同じオブジェクトで、[`RequestEvent`](/docs/kit/@sveltejs-kit#RequestEvent) のインスタンスです。

便利なプロパティやメソッドを数多く持っており、いくつかはすでに見たことがあるでしょう:

- `cookies` — [cookies API](cookies)
- `fetch` — 標準の [Fetch API](https://developer.mozilla.org/ja/docs/Web/API/Fetch_API) と同等ですが、いくつかの機能が追加されています
- `getClientAddress()` — クライアントの IP アドレスを取得する関数
- `isDataRequest` — クライアントサイドナビゲーション中にブラウザがデータをリクエストしていると `true`、ページやルート(route)が直接リクエストされていると `false`
- `locals` — 任意のデータを置く場所
- `params` — ルート(route)のパラメータ
- `request` — [Request](https://developer.mozilla.org/ja/docs/Web/API/Request) オブジェクト
- `route` — マッチしたルート(route)を表す `id` プロパティを持つオブジェクト
- `setHeaders(...)` — レスポンスに [HTTP ヘッダーを設定する](headers)関数
- `url` — 現在のリクエストを表す [URL](https://developer.mozilla.org/ja/docs/Web/API/URL) オブジェクト

便利なパターンとしては、`handle` で `event.locals` にデータを追加して、後続の `load` 関数でそれを使用できるようにすることです:

```js
/// file: src/hooks.server.js
export async function handle({ event, resolve }) {
	+++event.locals.answer = 42;+++
	return await resolve(event);
}
```

```js
/// file: src/routes/+page.server.js
export function load(+++event+++) {
	return {
		message: `the answer is ${+++event.locals.answer+++}`
	};
}
```
