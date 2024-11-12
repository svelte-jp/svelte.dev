---
title: Universal load functions
---

[以前学習した loading のセクション](page-data)では、`+page.server.js` と `+layout.server.js` ファイルを使ってサーバーからデータを取得しました。データベースから直接データを取得したり、cookie から読み取ったりするのにとても便利です。

しかし、クライアントサイドナビゲーションを行うとき、サーバーからデータを取得することが理にかなっていないケースもあります。例えば:

- 外部の API からデータを取得する
- インメモリデータが使えるならそれを使いたい
- ポップインを避けるため、画像がプリロードされるまでナビゲーションを遅らせたい
- コンポーネントや store など、シリアライズできないもの (SvelteKit は [devalue](https://github.com/Rich-Harris/devalue) でサーバーのデータを JSON に変換しています) を `load` から返す必要がある

この演習では、最後のケースを扱います。`src/routes/red/+page.server.js`、`src/routes/green/+page.server.js`、`src/routes/blue/+page.server.js` の server `load` 関数は、シリアライズできない `component` コンストラクタを返します。`/red`、`/green`、`/blue` に移動すると、ターミナルで 'Data returned from `load` ... is not serializable' というエラーが表示されるでしょう。

server `load` 関数を universal `load` 関数に変えるため、各 `+page.server.js` ファイルを `+page.js` にリネームします。これで、この関数はサーバーサイドレンダリング中にサーバーで実行されるものの、アプリのハイドレーション中またはユーザーがクライアントサイドナビゲーションを実行しているときにも実行されるようになります。

これで、他の値と同じように、`load` 関数から返された `component` を `src/routes/+layout.svelte` で使えるようになりました:

```svelte
/// file: src/routes/+layout.svelte
<nav
	class:has-color={!!$page.data.color}
	style:background={$page.data.color ?? 'var(--bg-2)'}
>
	<a href="/">home</a>
	<a href="/red">red</a>
	<a href="/green">green</a>
	<a href="/blue">blue</a>

+++	{#if $page.data.component}
		<svelte:component this={$page.data.component} />
	{/if}+++
</nav>
```

server `load` 関数と universal `load` 関数の違いや、その使い分けなど、詳細については[ドキュメント](https://kit.svelte.jp/docs/load#universal-vs-server)をご参照ください。
