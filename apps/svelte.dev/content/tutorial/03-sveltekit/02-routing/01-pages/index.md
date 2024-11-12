---
title: Pages
---

SvelteKit はファイルシステムベースのルーティング(Routing)を採用しており、アプリの _ルート(routes)_ (言い換えると、ユーザーが特定の URL に移動したときにアプリがすべきこと) については、コードベースのディレクトリで定義します。

`src/routes` 内にあるすべての `+page.svelte` ファイルは、アプリのページを作成します。このアプリでは、現在ページが1つあり (`src/routes/+page.svelte`)、これは `/` にマッピングされます。`/about` に移動すると、404 Not Found error となるでしょう。

それを修正しましょう。2つ目のページとして `src/routes/about/+page.svelte` を追加し、`src/routes/+page.svelte` の内容をコピーし、それで更新します:

```svelte
/// file: src/routes/about/+page.svelte
<nav>
	<a href="/">home</a>
	<a href="/about">about</a>
</nav>

<h1>+++about+++</h1>
<p>this is the +++about+++ page.</p>
```

これによって `/` と `/about` の間を移動できるようになりました。

> [!NOTE] 従来のマルチページアプリとは違い、`/about` に移動してから戻ると、シングルページアプリのように現在のページのコンテンツが更新されます。これにより、サーバーレンダリングによるスタートアップと、瞬時のナビゲーションという、両方の長所を得ることができます。(この動作は[設定で変更できます](/docs/kit/page-options)。)
