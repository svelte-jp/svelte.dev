---
title: .svelte ファイル 
---

コンポーネントは Svelte アプリケーションの構成要素です。これらは `.svelte` ファイルに書かれ、HTML のスーパーセットを使って記述されます。

以下の3つのセクション — script, styles, markup — は任意です。

<!-- prettier-ignore -->
```svelte
/// file: MyComponent.svelte
<script module>
	// モジュールレベルのロジックはここに書きます
	// (ほとんど使うことはありません)
</script>

<script>
	// インスタンスレベルのロジックはここに書きます
</script>

<!-- マークアップ (0行以上) はここに書きます -->

<style>
	/* スタイルはここに書きます */
</style>
```

## `<script>`

`<script>` ブロックは、コンポーネントインスタンスが作成されたときに実行される JavaScript (または `lang="ts` 属性を追加した時の　TypeScript) を含みます。トップレベルで宣言 (またはインポート) された変数は、コンポーネントのマークアップで参照できます。

通常のJavaScriptに加えて、_runes_ を使用して[コンポーネントのプロパティ]($props)を宣言したり、コンポーネントにリアクティビティを追加したりできます。Runes については次のセクションで説明します。

<!-- TODO describe behaviour of `export` -->

## `<script module>`

`<script>` タグに `module` 属性を付けると、モジュールが最初に評価される際に1回だけ実行され、各コンポーネントインスタンスごとに実行されるわけではありません。このブロックで宣言された変数は、コンポーネント内の他の場所から参照できますが、その逆はできません。

```svelte
<script module>
	let total = 0;
</script>

<script>
	total += 1;
	console.log(`instantiated ${total} times`);
</script>
```

You can `export` bindings from this block, and they will become exports of the compiled module. You cannot `export default`, since the default export is the component itself.

このブロックから `export` バインディングを使用してエクスポートすることができ、それらはコンパイルされたモジュールのエクスポートとして扱われます。ただし、コンポーネント自体にデフォルトエクスポートがされるため `export default` は使用できません。

> [!NOTE] If you are using TypeScript and import such exports from a `module` block into a `.ts` file, make sure to have your editor setup so that TypeScript knows about them. This is the case for our VS Code extension and the IntelliJ plugin, but in other cases you might need to setup our [TypeScript editor plugin](https://www.npmjs.com/package/typescript-svelte-plugin).

> [!NOTE] TypeScriptを使用していて、`module` ブロックからエクスポートされたものを　`.ts` ファイルにインポートする場合は、TypeScriptがそれらを認識できるようにエディタの設定を行う必要があります。VS Code拡張機能やIntelliJプラグインを使用している場合はこの設定が必要となりますが、それ以外の場合は [TypeScript エディタープラグイン](https://www.npmjs.com/package/typescript-svelte-plugin) を設定する必要がある場合があります。

> [!LEGACY]
> Svelte 4 では、このスクリプトタグは `<script context="module">` を使用して作成されました。

## `<style>`

`<style>` ブロック内のCSSは、そのコンポーネントにスコープされます。

```svelte
<style>
	p {
		/* これはこのコンポネント内の <p> 要素にのみ影響します */
		color: burlywood;
	}
</style>
```

詳細については、[スタイリング](scoped-styles) のセクションをご覧ください。
