---
title: Optional parameters
---

[ルーティング(Routing)](/tutorial/kit/pages) の最初の章で、[動的なパラメータ](/tutorial/kit/params)付きのルート(routes)を作成する方法について学習しました。

パラメータをオプショナルにできたら便利なときがあるでしょう。その代表的な例は、ロケールを決めるのにパス名を使用する場合です — `/fr/...`、`/de/...` などなど — このとき、デフォルトのロケールも持ちたいはずです。

そうするには、二重括弧を使用します。`[lang]` ディレクトリを `[[lang]]` にリネームしましょう。

今は `src/routes/+page.svelte` と `src/routes/[[lang]]/+page.svelte` がどちらも `/` にマッチするため、アプリがビルドに失敗します。`src/routes/+page.svelte` を削除してください (エラーページから復帰するには、アプリをリロードする必要があるかもしれません)。

最後に、`src/routes/[[lang]]/+page.server.js` を編集してデフォルトロケールを指定してください。

```js
/// file: src/routes/[[lang]]/+page.server.js
const greetings = {
	en: 'hello!',
	de: 'hallo!',
	fr: 'bonjour!'
};

export function load({ params }) {
	return {
		greeting: greetings[params.lang +++?? 'en'+++]
	};
}
```
