---
title: $env/static/private
---

API キーやデータベースの認証情報などの環境変数は `.env` ファイルに追加することでき、アプリケーションから使えるようになります。

> [!NOTE] また、`.env.local` ファイルや `.env.[mode]` ファイルも使えます — 詳細は [Vite のドキュメント](https://vitejs.dev/guide/env-and-mode.html#env-files) をご覧ください。機密情報を含むファイルは必ず `.gitignore` ファイルに追加してください！
>
> `process.env` にある環境変数も `$env/static/private` 経由で使うことができます。

この演習では、環境変数を使って、正しいパスフレーズを知っているユーザーのみ web サイトを見ることができるようにしたいと思います。

まず、`.env` に新しい環境変数を追加します。

```env
/// file: .env
PASSPHRASE=+++"open sesame"+++
```

`src/routes/+page.server.js` を開いてください。`$env/static/private` から `PASSPHRASE` をインポートし、[form action](/tutorial/kit/the-form-element) の中でそれを使用してください。

```js
/// file: src/routes/+page.server.js
import { redirect, fail } from '@sveltejs/kit';
+++import { PASSPHRASE } from '$env/static/private';+++

export function load({ cookies }) {
	if (cookies.get('allowed')) {
		redirect(307, '/welcome');
	}
}

export const actions = {
	default: async ({ request, cookies }) => {
		const data = await request.formData();

		if (data.get('passphrase') === +++PASSPHRASE+++) {
			cookies.set('allowed', 'true', {
				path: '/'
			});

			redirect(303, '/welcome');
		}

		return fail(403, {
			incorrect: true
		});
	}
};
```

正しいパスフレーズを知っている人が、web サイトにアクセスできるようになりました。

## Keeping secrets

機密データが誤ってブラウザに送信されるとハッカーや悪者に簡単に盗まれてしまうので、そうならないようにすることが重要です。

SvelteKit では、これを簡単に防ぐことができます。もし `PASSPHRASE` を `src/routes/+page.svelte` にインポートしようとしたらどうなるか確認してみましょう。

```svelte
/// file: src/routes/+page.svelte
<script>
	+++import { PASSPHRASE } from '$env/static/private';+++
	let { form } = $props();
</script>
```

エラーオーバーレイが表示され、`$env/static/private` はクライアントサイドコードにインポートできないことを教えてくれます。これはサーバーモジュールにのみインポートすることができます。

- `+page.server.js`
- `+layout.server.js`
- `+server.js`
- `.server.js` で終わるモジュール
- `src/lib/server` に置いてあるモジュール

同様に、これらのモジュールは他のサーバーモジュールにのみインポートすることができます。

## Static vs dynamic

`$env/static/private` にある `static` とは、これらの値がビルド時に解決され、 _静的に置き換えられる_ ということを示しています。これによって最適化が可能になります。

```js
import { FEATURE_FLAG_X } from '$env/static/private';

if (FEATURE_FLAG_X === 'enabled') {
	// FEATURE_FLAG_X が enabled でない場合、
	// ここにあるコードはビルド出力から削除されます
}
```

場合によっては、 _動的_ な環境変数 — 言い換えると、アプリの実行時までわからない環境変数を参照する必要があるかもしれません。これについては、次の演習で説明します。
