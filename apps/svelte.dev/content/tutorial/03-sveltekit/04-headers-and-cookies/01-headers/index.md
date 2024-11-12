---
title: Setting headers
---

`load` 関数の中では (後で学習する [form actions](the-form-element)、[hooks](handle)、[API routes](get-handlers)も同様)、`setHeaders` 関数を使用することができます。これは — 驚くことではありませんが — レスポンスにヘッダーをセットすることができます。

一般的には、[`Cache-Control`](https://developer.mozilla.org/ja/docs/Web/HTTP/Headers/Cache-Control) レスポンスヘッダーでキャッシュの挙動をカスタマイズするのに使用したりします。ただしこのチュートリアルでは、あまり推奨されないけれど、よりわかりやすいことをやってみましょう:

```js
/// file: src/routes/+page.server.js
export function load(+++{ setHeaders }+++) {
+++	setHeaders({
		'Content-Type': 'text/plain'
	});+++
}
```

(この効果を確認するには、iframe をリロードする必要があるかもしれません。)
