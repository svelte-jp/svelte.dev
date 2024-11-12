---
title: Redirects
---

`throw` のメカニズムを、あるページから別のページにリダイレクトするのにも使えます。

`load` 関数を `src/routes/a/+page.server.js` に作成してください。

```js
/// file: src/routes/a/+page.server.js
import { redirect } from '@sveltejs/kit';

export function load() {
	redirect(307, '/b');
}
```

`/a` に移動しようとすると、`/b` に直行するようになります。

`redirect(...)` は、`load` 関数、form actions、API ルート、そして後の章で説明する `handle` hook の内側で使うことができます。

よく使用されるステータスコードはこちらです。

- `303` — form actions で、送信に成功したあと続いて使用されます
- `307` — 一時的なリダイレクトに使用されます
- `308` — 恒久的なリダイレクトに使用されます
