---
title: The <form> element
---

[loading data](page-data) の章では、データをサーバーからブラウザに取得してくる方法を見てきました。時には、その逆方向にデータを送信する必要があります。そこで、web プラットフォームにおけるデータ送信方法である `<form>` の登場です。

todo アプリを作ってみましょう。すでに `src/lib/server/database.js` にセットアップ済みのインメモリデータベースがあり、`src/routes/+page.server.js` の `load` 関数で [`cookies`](https://kit.svelte.jp/docs/load#cookies) API を使用しているためユーザーごとの todo リストを持つことができるようになっています。ここでは新しい todo を作成するための `<form>` を追加する必要があります。

```svelte
/// file: src/routes/+page.svelte
<h1>todos</h1>

+++<form method="POST">
	<label>
		add a todo:
		<input
			name="description"
			autocomplete="off"
		/>
	</label>
</form>+++

<ul class="todos">
```

追加した `<input>` になにか入力して Enter を押すと、ブラウザは現在のページに対する POST リクエストを作成します (`method="POST"` 属性があるため)。リクエストの結果がエラーになっているのは、その POST リクエストを処理するためのサーバーサイドの _action_ が作成されていないからです。では、それをやってみましょう。

```js
/// file: src/routes/+page.server.js
import * as db from '$lib/server/database.js';

export function load({ cookies }) {
	// ...
}

+++export const actions = {
	default: async ({ cookies, request }) => {
		const data = await request.formData();
		db.createTodo(cookies.get('userid'), data.get('description'));
	}
};+++
```

`request` は標準の [Request](https://developer.mozilla.org/ja/docs/Web/API/Request) オブジェクトです; `await request.formData()` は [`FormData`](https://developer.mozilla.org/ja/docs/Web/API/FormData) インスタンスを返します。

Enter を押すと、データベースが更新され、新しいデータでページがリロードします。

`fetch` コードなどを書く必要がなかったこと、データが自動的に更新されることにご注目ください。そして、`<form>` 要素を使用しているため、このアプリはたとえ JavaScript が無効または利用できない場合でも動作します。
