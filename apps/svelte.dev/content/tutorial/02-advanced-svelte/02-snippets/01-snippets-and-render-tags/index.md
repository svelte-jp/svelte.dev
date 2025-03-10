---
title: Snippets and render tags
---

スニペットを使用すると、別のファイルに抽出することなく、コンポーネント内のコンテンツを再利用できます。

この演習では、[三猿](https://en.wikipedia.org/wiki/Three_wise_monkeys)の表と、それぞれの Unicode エスケープ シーケンスおよび HTML エンティティを作成します。今のところ、猿は 1 匹だけです。

もちろん、マークアップを複製することもできます。または、`{ emoji, description }` オブジェクトの配列を作成し、それを `{#each ...}` ブロックに渡すこともできます。しかし、よりすっきりした解決策は、マークアップを再利用可能なブロックにカプセル化することです。

まず、_スニペットを宣言_ します。

```svelte
/// file: App.svelte
+++{#snippet monkey()}+++
	<tr>
		<td>{emoji}</td>
		<td>{description}</td>
		<td>\u{emoji.charCodeAt(0).toString(16)}\u{emoji.charCodeAt(1).toString(16)}</td>
		<td>&amp#{emoji.codePointAt(0)}</td>
	</tr>
+++{/snippet}+++
```

猿はレンダリングするまで見えません。レンダリングしてみましょう。

```svelte
/// file: App.svelte
<tbody>
	{#snippet monkey()}...{/snippet}

	+++{@render monkey()}+++
</tbody>
```

残りの猿に対してスニペットを使用する前に、スニペットにデータを渡す必要があります。スニペットには 0 個以上のパラメータを指定できます。

```svelte
/// file: App.svelte
<tbody>
	+++{#snippet monkey(emoji, description)}...{/snippet}+++

	+++{@render monkey('🙈', 'see no evil')}+++
</tbody>
```

> [!NOTE] 必要に応じて、デストラクチャパラメータを使用することもできます。

残りの猿を追加します。

- `'🙈', 'see no evil'`
- `'🙉', 'hear no evil'`
- `'🙊', 'speak no evil'`

最後に、不要になった `<script>` ブロックを削除します。

```svelte
/// file: App.svelte
---<script>
	let emoji = '🙈';
	let description = 'see no evil';
</script>---
```

> [!NOTE] スニペットはコンポーネント内のどこにでも宣言できますが、関数と同様に、同じ「スコープ」または子スコープ内のレンダリングタグに対してのみ使用できます。
