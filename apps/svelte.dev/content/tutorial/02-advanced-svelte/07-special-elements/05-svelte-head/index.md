---
title: <svelte:head>
---

`<svelte:head>` 要素を使うと、document の `<head>` 内に要素を挿入することができます。これは SEO を良くするのに不可欠な `<title>` タグや `<meta>` タグなどに有用です。

このチュートリアルでその用途の使用例を示すのは難しいので、別の用途で使ってみましょう — スタイルシートを読み込みます。

```svelte
/// file: App.svelte
<script>
	const themes = ['margaritaville', 'retrowave', 'spaaaaace', 'halloween'];
	let selected = $state(themes[0]);
</script>

+++<svelte:head>
	<link rel="stylesheet" href="/tutorial/stylesheets/{selected}.css" />
</svelte:head>+++

<h1>Welcome to my site!</h1>
```

> [!NOTE] サーバサイドレンダリング (SSR) モードでは、`<svelte:head>` の内容は HTML の他の部分とは別に返されます。
