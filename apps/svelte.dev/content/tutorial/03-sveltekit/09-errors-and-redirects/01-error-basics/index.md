---
title: Basics
---

SvelteKit には2種類のエラーがあります — _想定される(expected)_ エラーと _予期せぬ(unexpected)_ エラーです。

想定されるエラーとは、`@sveltejs/kit` からインポートできる [`error`](/docs/kit/@sveltejs-kit#error) ヘルパーを使用して作成されるエラーのことです。`src/routes/expected/+page.server.js` をご覧ください。

```js
/// file: src/routes/expected/+page.server.js
import { error } from '@sveltejs/kit';

export function load() {
	error(420, 'Enhance your calm');
}
```

それ以外のエラー — 例えば `src/routes/unexpected/+page.server.js` にあるようなエラー — は、予期せぬエラーとして扱われます。

```js
/// file: src/routes/unexpected/+page.server.js
export function load() {
	throw new Error('Kaboom!');
}
```

想定されるエラーをスローすることは、あなたが SvelteKit に '大丈夫、ここで何をやってるかちゃんとわかってるから' と伝えているようなものです。対照的に、予期せぬエラーの場合は、アプリのバグであると考えられます。予期せぬエラーがスローされた場合、そのメッセージとスタックトレースがコンソールにログ出力されるでしょう。

> [!NOTE] 後の章で、`handleError` hook を使用したカスタムエラーハンドリングの追加方法を学習します。

このアプリのリンクをクリックすると、重要な違いに気付くでしょう。想定されるエラーのメッセージはユーザーに表示されますが、予期せぬエラーのメッセージは編集され、一般的な 'Internal Error' メッセージと 500 ステータスコードに置き換えられます。これは、エラーメッセージには機密情報が含まれている可能性があるからです。
