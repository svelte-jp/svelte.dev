---
title: page
---

> TODO link to stores exercise

以前学んだように、Svelte の store は個々のコンポーネントに属さないデータを置くことができます。

SvelteKit では、3つの読み取り専用 store を `$app/stores` モジュールから使用できます — `page`、`navigating`、`updated` です。もっとも多く使用することになるのは [`page`](https://kit.svelte.jp/docs/types#public-types-page) で、これは現在のページに関する情報を取得することができます:

- `url` — 現在のページの [URL](https://developer.mozilla.org/ja/docs/Web/API/URL)
- `params` — 現在のページの[パラメータ](params)
- `route` — 現在のルート(route)を表す `id` プロパティを持つオブジェクト
- `status` — 現在のページの HTTP ステータスコード
- `error` — 現在のページのエラーオブジェクト (エラーが存在する場合。[以降](error-basics)の[演習](handleerror)でエラーハンドリングを学習する予定です)
- `data` — 現在のページの data。全ての `load` 関数からの戻り値が足されたもの
- `form` — [form action](the-form-element) から返されるデータ

他の store と同様、コンポーネントでは `$` シンボルを先頭に付けることでその値を参照することができます。例えば、現在のパス名は `$page.url.pathname` でアクセスできます:

```svelte
/// file: src/routes/+layout.svelte
<script>
	+++import { page } from '$app/stores';+++

	let { children } = $props();
</script>

<nav>
	<a href="/" +++aria-current={$page.url.pathname === '/'}+++>
		home
	</a>

	<a href="/about" +++aria-current={$page.url.pathname === '/about'}+++>
		about
	</a>
</nav>

{@render children()}
```
