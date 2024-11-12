---
title: Your first component
---

Svelteでは、アプリケーションは1つ以上の _コンポーネント_ で構成されます。コンポーネントとは、HTML、CSS、JavaScript をカプセル化した再利用可能な自己完結型のコードブロックのことで、`.svelte` ファイルに記述します。右のコードエディタにある `App.svelte` は単純なコンポーネントの例です。

## Adding data

静的なマークアップ(HTML)をレンダリングするだけのコンポーネントは面白くありません。いくつかデータを追加してみましょう。

まず、`script` タグを追加してその中に `name` 変数を宣言します。

```svelte
/// file: App.svelte
+++<script>
	let name = 'Svelte';
</script>+++

<h1>Hello world!</h1>
```

次に、マークアップから `name` を参照します。

```svelte
/// file: App.svelte
<h1>Hello +++{name}+++!</h1>
```

中括弧`{}`の中には JavaScript のコードを置くことができます。中括弧の中の `name` を `name.toUpperCase()` に置き換えてみましょう。

```svelte
/// file: App.svelte
<h1>Hello {name+++.toUpperCase()+++}!</h1>
```
