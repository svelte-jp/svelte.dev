---
title: Route parameters
path: /blog
---

動的なパラメータ付きのルート(routes)を作成するには、角括弧を使用して有効な変数名を囲みます。例えば、`src/routes/blog/[slug]/+page.svelte` というファイルは、`/blog/one`、`/blog/two`、`/blog/three` などにマッチするルート(route)を作成します。

そのファイルを作成してみましょう。

```svelte
/// file: src/routes/blog/[slug]/+page.svelte
<h1>blog post</h1>
```

これで、`/blog` ページから個々のブログ記事に移動できるようになりました。次の章では、そのコンテンツをロードする方法を見ていきます。

> [!NOTE] 少なくとも1つの静的な文字で区切られていれば、1つの URL セグメント内に複数のルートパラメータを使用することができます。`foo/[bar]x[baz]` は有効なルートで、`[bar]` と `[baz]` は動的なパラメータです。
