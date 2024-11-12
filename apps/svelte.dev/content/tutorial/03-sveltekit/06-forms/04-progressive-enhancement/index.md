---
title: Progressive enhancement
---

私たちは `<form>` を使用しているため、たとえユーザーが JavaScript を使えなくても ([これはあなたが思うより頻繁に発生しています](https://kryogenix.org/code/browser/everyonehasjs.html)) アプリが動作します。これは素晴らしいことです、なぜなら私たちのアプリがレジリエントであることを意味するからです。

ほとんどの場合、ユーザーは JavaScript を有効にしています。そのような場合は、SvelteKit がクライアントサイドルーティングで `<a>` 要素を _漸進的に強化(progressively enhance)_ しているのと同じように、form の体験を漸進的に強化することができます。

`$app/forms` から `enhance` 関数をインポートし…

```svelte
/// file: src/routes/+page.svelte
<script>
	+++import { enhance } from '$app/forms';+++

	let { data, form } = $props();
</script>
```

…そして `use:enhance` ディレクティブを `<form>` 要素に追加します。

```svelte
/// file: src/routes/+page.svelte
<form method="POST" action="?/create" +++use:enhance+++>
```

```svelte
/// file: src/routes/+page.svelte
<form method="POST" action="?/delete" +++use:enhance+++>
```

これだけです！ JavaScript が有効な場合、`use:enhance` は、ブラウザネイティブな動作(フルページリロードを除く)をエミュレートします。こうすると、

- `form` プロパティを更新します
- 成功レスポンスの場合は全てのデータを無効化・最新化(invalidate)するようマークし、`load` 関数を再実行させます
- リダイレクトレスポンスの場合は新しいページに移動します
- エラーが発生した場合は最も近くにあるエラーページをレンダリングします

こうして、ページをリロードするのではなく更新するようになったので、トランジションなどで装飾することができます。

```svelte
/// file: src/routes/+page.svelte
<script>
	+++import { fly, slide } from 'svelte/transition';+++
	import { enhance } from '$app/forms';

	let { data, form } = $props();
</script>
```

```svelte
/// file: src/routes/+page.svelte
<li +++in:fly={{ y: 20 }} out:slide+++>...</li>
```
