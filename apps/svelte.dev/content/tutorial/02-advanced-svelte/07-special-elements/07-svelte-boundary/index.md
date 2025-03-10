---
title: <svelte:boundary>
---

エラーによってアプリが壊れた状態になるのを防ぐために、`<svelte:boundary>` 要素を使用して、エラーを _エラー境界_ 内に封じ込めることができます。

この例では、`<FlakyComponent>` にバグが含まれています。ボタンをクリックすると、`mouse` が `null` に設定され、テンプレート内の `{mouse.x}` および `{mouse.y}` 式がレンダリングされなくなります。

理想的には、バグを修正するだけです。しかし、それが常に可能なわけではありません。コンポーネントが他の誰かの所有物である場合もあり、予期しない事態に備える必要がある場合もあります。まず、`<FlakyComponent />` を `<svelte:boundary>` でラップします。

```svelte
<!--- file: App.svelte --->
+++<svelte:boundary>+++
	<FlakyComponent />
+++</svelte:boundary>+++
```

境界でハンドラーが指定されていないため、これまでのところ何も変更されていません。エラーが発生したときに表示する UI を提供するために、`failed` [スニペット](snippets-and-render-tags) を追加します。

```svelte
<!--- file: App.svelte --->
<svelte:boundary>
	<FlakyComponent />

+++	{#snippet failed(error)}
		<p>Oops! {error.message}</p>
	{/snippet}+++
</svelte:boundary>
```

これで、ボタンをクリックすると、境界の内容がスニペットに置き換えられます。`failed` に渡された 2 番目の引数を利用してリセットを試みることができます。

```svelte
<!--- file: App.svelte --->
<svelte:boundary>
	<FlakyComponent />

	{#snippet failed(error+++, reset+++)}
		<p>Oops! {error.message}</p>
		+++<button onclick={reset}>Reset</button>+++
	{/snippet}
</svelte:boundary>
```

また、`failed` スニペットに渡されるのと同じ引数で呼び出される `onerror` ハンドラを指定することもできます。

```svelte
<!--- file: App.svelte --->
<svelte:boundary +++onerror={(e) => console.error(e)}+++>
	<FlakyComponent />

	{#snippet failed(error, reset)}
		<p>Oops! {error.message}</p>
		<button onclick={reset}>Reset</button>
	{/snippet}
</svelte:boundary>
```

これは、エラーに関する情報をレポート サービスに送信したり、エラー境界自体の外側に UI を追加したりする場合に役立ちます。
