---
title: handleError
---

`handleError` hook は、予期せぬエラー(unexpected errors)をインターセプトし、何らかの動作をトリガーすることができます。例えば、エラーが起きたときに Slack channel に通知したり、エラーロギングサービスにデータを送ったりします。

[前の演習](error-basics)を振り返ると、`@sveltejs/kit` からインポートする `error` ヘルパーで作成されていないエラーは、 _予期せぬ(unexpected)_ エラーです。それは通常、アプリを修正する必要があるということです。デフォルトの動作としては、エラーをログに記録します:

```js
/// file: src/hooks.server.js
export function handleError({ event, error }) {
	console.error(error.stack);
}
```

`/the-bad-place` に移動すると、この動作を見ることができます — エラーページが表示され、(URL バーの右にあるボタンを押して) ターミナルを開くと `src/routes/the-bad-place/+page.server.js` からのメッセージが表示されているはずです。

エラーメッセージをユーザーに表示していないことにご注目ください。これは、エラーメッセージには機密情報が含まれている可能性があり、ユーザーを混乱させ、最悪の場合、悪意のある人間に利用される可能性があるからです。そのため、アプリケーションで利用できるエラーオブジェクト (`+error.svelte` ページでは `$page.error`、`src/error.html` フォールバック では `%sveltekit.error%`) はこれだけです:

<!-- prettier-ignore-start -->
```js
{
	message: 'Internal Error' // or 'Not Found' for a 404
}
```
<!-- prettier-ignore-end -->

状況によっては、このオブジェクトをカスタマイズしたいでしょう。そのためには、`handleError` からオブジェクトを返します:

```js
/// file: src/hooks.server.js
export function handleError({ event, error }) {
	console.error(error.stack);

	return {
		message: 'everything is fine',
		code: 'JEREMYBEARIMY'
	};
}
```

カスタムのエラーページで `message` 以外のプロパティを参照できるようになりました。`src/routes/+error.svelte` を作成しましょう:

```svelte
/// file: src/routes/+error.svelte
<script>
	import { page } from '$app/stores';
</script>

<h1>{$page.status}</h1>
<p>{$page.error.message}</p>
<p>error code: {$page.error.code}</p>
```
