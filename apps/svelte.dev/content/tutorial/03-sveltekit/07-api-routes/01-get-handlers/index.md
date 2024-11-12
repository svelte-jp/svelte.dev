---
title: GET handlers
---

SvelteKit では、ページ以外にも様々なものを作ることができます。`+server.js` ファイルを追加し、そこでHTTP メソッド `GET`、`PUT`、`POST`、`PATCH`、`DELETE` に対応する関数をエクスポートすることで、 _API ルート(API routes)_ を作成することもできます。

このアプリは、ボタンをクリックしたときに `/roll` API ルートからデータを取得します。`src/routes/roll/+server.js` ファイルを追加し、そのルートを作成しましょう。

```js
/// file: src/routes/roll/+server.js
export function GET() {
	const number = Math.floor(Math.random() * 6) + 1;

	return new Response(number, {
		headers: {
			'Content-Type': 'application/json'
		}
	});
}
```

これでボタンクリックしたときの動作が動くようになりました。

リクエストハンドラは [Response](https://developer.mozilla.org/ja/docs/Web/API/Response/Response) オブジェクトを返さなければなりません。API ルートから JSON を返すことはよくあることなので、SvelteKit はこのようなレスポンスを生成する便利な関数を提供しています。

```js
/// file: src/routes/roll/+server.js
+++import { json } from '@sveltejs/kit';+++

export function GET() {
	const number = Math.floor(Math.random() * 6) + 1;

---	return new Response(number, {
		headers: {
			'Content-Type': 'application/json'
		}
	});---
+++	return json(number);+++
}
```
