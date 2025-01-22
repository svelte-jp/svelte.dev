---
title: page
---

SvelteKit では、3つの読み取り専用 state オブジェクトを `$app/state` モジュールから使用できます — `page`、`navigating`、`updated` です。もっとも多く使用することになるのは [`page`](/docs/kit/@sveltejs-kit#Page) で、これは現在のページに関する情報を取得することができます:

- `url` — 現在のページの [URL](https://developer.mozilla.org/ja/docs/Web/API/URL)
- `params` — 現在のページの[パラメータ](params)
- `route` — 現在のルート(route)を表す `id` プロパティを持つオブジェクト
- `status` — 現在のページの HTTP ステータスコード
- `error` — 現在のページのエラーオブジェクト (エラーが存在する場合。[以降](error-basics)の[演習](handleerror)でエラーハンドリングを学習する予定です)
- `data` — 現在のページの data。全ての `load` 関数からの戻り値が足されたもの
- `form` — [form action](the-form-element) から返されるデータ

これらの各プロパティはリアクティブで、内部的には `$state.raw` が使用されています。これは `page.url.pathname` を使用する例です:

```svelte
/// file: src/routes/+layout.svelte
<script>
	+++import { page } from '$app/state';+++

	let { children } = $props();
</script>

<nav>
	<a href="/" +++aria-current={page.url.pathname === '/'}+++>
		home
	</a>

	<a href="/about" +++aria-current={page.url.pathname === '/about'}+++>
		about
	</a>
</nav>

{@render children()}
```

> [!NOTE] Prior to SvelteKit 2.12, you had to use `$app/stores` for this, which provides a `$page` store with the same information. If you're currently using `$app/stores`, we advise you to migrate towards `$app/state` (requires Svelte 5).
