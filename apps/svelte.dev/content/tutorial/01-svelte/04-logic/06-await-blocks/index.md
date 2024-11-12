---
title: Await blocks
---

ほとんどの webアプリケーションでは、どこかの時点で非同期のデータを扱わなければなりません。Svelte ではマークアップの中で直接 [promises](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Using_promises) の値を簡単に _await_ することができます。

```svelte
/// file: App.svelte
+++{#await promise}+++
	<p>...rolling</p>
+++{:then number}
	<p>you rolled a {number}!</p>
{:catch error}
	<p style="color: red">{error.message}</p>
{/await}+++
```

> [!NOTE] 直近の `promise` だけが処理されるので、レースコンディション(race conditions)を気にする必要はありません。

promise が reject できないことがわかっている場合は、`catch` ブロックを省略することができます。また promise が resolve するまで何も表示したくない場合は、最初のブロックを省略することもできます。

```svelte
{#await promise then number}
	<p>you rolled a {number}!</p>
{/await}
```
