---
title: Route groups
---

[ルーティング(Routing)のイントロダクション](/tutorial/kit/layouts)で見たように、レイアウトによって UI とデータをロードするロジックを異なるルート(routes)間で共有することができます。

ルート(route)に影響することなく、レイアウトを使うことができたら便利なときがあるでしょう — 例えば、`/app` ルートと `/account` ルートは認証の背後に置く必要があり、`/about` ページは世界に公開する、ということがあるかもしれません。これを行うには、 _ルートグループ(route group)_ を使います。これは、丸括弧でくくられたディレクトリです。

`account` を `(authed)/account` にリネームして `(authed)` グループを作成し、それから `app` を `(authed)/app` にリネームします。

`src/routes/(authed)/+layout.server.js` を作成することで、これらのルート(routes)のアクセスをコントロールすることができます。

```js
/// file: src/routes/(authed)/+layout.server.js
import { redirect } from '@sveltejs/kit';

export function load({ cookies, url }) {
	if (!cookies.get('logged_in')) {
		redirect(303, `/login?redirectTo=${url.pathname}`);
	}
}
```

これらのページにアクセスしようとすると、`/login` ルート(route)にリダイレクトされます。このルートには、`src/routes/login/+page.server.js` に、`logged_in` cookie をセットする form action があります。

また、`src/routes/(authed)/+layout.svelte` ファイルを追加することで、これら2つのルートに UI を追加することができます。

```svelte
/// file: src/routes/(authed)/+layout.svelte
<script>
	let { children } = $props();
</script>

{@render children()}

<form method="POST" action="/logout">
	<button>log out</button>
</form>
```
