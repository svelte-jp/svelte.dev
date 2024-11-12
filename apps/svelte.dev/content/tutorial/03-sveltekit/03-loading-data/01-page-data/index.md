---
title: Page data
path: /blog
---

本質的には、SvelteKit が行う仕事は次の3つに集約されます。

1. **ルーティング(Routing)** — 受け取ったリクエストにどのルートがマッチするかを判断する
2. **ローディング(Loading)** — ルートが必要とするデータを取得する
3. **レンダリング(Rendering)** — (サーバー上で) HTML を生成する、または (ブラウザで) DOMを更新する

これまで、ルーティングとレンダリングがどのように動作するか見てきました。ここではその中間のローディングについて説明します。

アプリの全てのページで、`+page.svelte` ファイルと同じ並びに `+page.server.js` ファイルを置き、そこで `load` 関数を宣言することができます。ファイル名が示す通り、このモジュールはサーバーでのみ実行されます (クライアントサイドナビゲーション中であっても)。`src/routes/blog/+page.server.js` ファイルを追加しましょう。そうすることで、`src/routes/blog/+page.svelte` にあるハードコードされたリンクを、実際のブログ記事データで置き換えることができるようになります。

```js
/// file: src/routes/blog/+page.server.js
import { posts } from './data.js';

export function load() {
	return {
		summaries: posts.map((post) => ({
			slug: post.slug,
			title: post.title
		}))
	};
}
```

> [!NOTE] このチュートリアルでは、`src/routes/blog/data.js` からデータをインポートしています。現実のアプリでは、データベースや CMS からデータをロードすることが多いかと思いますが、今このチュートリアルではこのようにしています。

このデータは `src/routes/blog/+page.svelte` で `data` prop を介してアクセスすることができます。

```svelte
/// file: src/routes/blog/+page.svelte
+++<script>
	let { data } = $props();
</script>+++

<h1>blog</h1>

<ul>
---	<li><a href="/blog/one">one</a></li>
	<li><a href="/blog/two">two</a></li>
	<li><a href="/blog/three">three</a></li>---
+++	{#each data.summaries as { slug, title }}
		<li><a href="/blog/{slug}">{title}</a></li>
	{/each}+++
</ul>
```

では、記事のページでも同じようにやってみましょう。

```js
/// file: src/routes/blog/[slug]/+page.server.js
import { posts } from '../data.js';

export function load({ params }) {
	const post = posts.find((post) => post.slug === params.slug);

	return {
		post
	};
}
```

```svelte
/// file: src/routes/blog/[slug]/+page.svelte
+++<script>
	let { data } = $props();
</script>+++

---<h1>blog post</h1>---
+++<h1>{data.post.title}</h1>
<div>{@html data.post.content}</div>+++
```

最後にもう1つやらなければならないことがあります — ユーザーが `/blog/nope` のような無効なパス名でアクセスするかもしれないため、その場合には 404 ページで応答するようにしたいです。

```js
/// file: src/routes/blog/[slug]/+page.server.js
+++import { error } from '@sveltejs/kit';+++
import { posts } from '../data.js';

export function load({ params }) {
	const post = posts.find((post) => post.slug === params.slug);

	+++if (!post) error(404);+++

	return {
		post
	};
}
```

エラーハンドリングの詳細については、後の章で学習します。
