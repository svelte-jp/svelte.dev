---
title: Reading and writing cookies
---

[`setHeaders`](headers) 関数は `Set-Cookie` ヘッダーのために使用することはできません。代わりに、`cookies` API を使用しましょう。

`load` 関数では、`cookies.get(name, options)` で cookie を読み取ることができます:

```js
/// file: src/routes/+page.server.js
export function load(+++{ cookies }+++) {
	+++const visited = cookies.get('visited');+++

	return {
		visited: visited === 'true'
	};
}
```

cookie を設定するには、`cookies.set(name, value, options)` を使用します。cookie を設定するときは `path` を明示的に設定することを強く推奨します。なぜなら、ブラウザのデフォルトの挙動は — 少し使い勝手が悪いのですが — 現在のパスの親に cookie を設定するからです。

```js
/// file: src/routes/+page.server.js
export function load({ cookies }) {
	const visited = cookies.get('visited');

	+++cookies.set('visited', 'true', { path: '/' });+++

	return {
		visited: visited === 'true'
	};
}
```

これで、iframe をリロードすると、`Hello stranger!` が `Hello friend!` になります。

`cookies.set(name, ...)` を呼び出すと `Set-Cookie` ヘッダーが書き込まれますが、cookie の内部の map も更新され、以降、同リクエスト中の `cookies.get(name)` は更新された値を返します。内部では、`cookies` API はポピュラーな `cookie` パッケージを使用しています — `cookies.get` と `cookies.set` に渡されるオプションは `cookie` の[ドキュメント](https://github.com/jshttp/cookie#api)にある `parse` オプションと `serialize` オプションに対応しています。SvelteKit では、cookie をセキュアにするために以下をデフォルトで設定しています:

```js
{
	httpOnly: true,
	secure: true,
	sameSite: 'lax'
}
```
