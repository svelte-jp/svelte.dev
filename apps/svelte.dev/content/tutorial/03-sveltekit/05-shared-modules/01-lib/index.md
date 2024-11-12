---
title: The $lib alias
---

SvelteKit はディレクトリベースのルーティングを使用しているので、モジュールやコンポーネントとそれを使用するルート(route)を一緒に配置するのがとても簡単です。経験則では、'コードは使う場所のすぐ近くに置く (put code close to where it's used)' です。 

コードが複数の場所で使われることもよくあります。そのときに、インポートのプレフィックスに `../../../../` をつけなくても全てのルート(route)からアクセスできる置き場所があると便利です。SvelteKit では、`src/lib` ディレクトリがその場所です。このディレクトリに配置されているものは、`$lib` エイリアスを介して `src` にあるどのモジュールからもアクセスすることができます。

この演習にある両方の `+page.svelte` ファイルは `src/lib/message.js` をインポートしています。しかし `/a/deeply/nested/route` に移動すると、アプリが壊れます。なぜなら、プレフィックスが間違っているからです。代わりに、 `$lib/message.js` を使用するように更新しましょう:

```svelte
/// file: src/routes/a/deeply/nested/route/+page.svelte
<script>
	import { message } from +++'$lib/message.js'+++;
</script>

<h1>a deeply nested route</h1>
<p>{message}</p>
```

`src/routes/+page.svelte` も同じようにしましょう:

```svelte
/// file: src/routes/+page.svelte
<script>
	import { message } from +++'$lib/message.js'+++;
</script>

<h1>home</h1>
<p>{message}</p>
```
