---
title: trailingSlash
---

2つの URL `/foo` と `/foo/` は同じように見えるかもしれませんが、実際は異なります。`./bar` のような相対 URL は、1つめのケースでは `/bar` に解決し、2つ目のケースでは `/foo/bar` に解決します。検索エンジンはこれらを別々のエントリとして扱うため、SEO に悪影響を与えます。

要するに、末尾のスラッシュを雑に扱うのは悪い考えだということです。デフォルトで、SvelteKit は末尾のスラッシュを削除します。つまり、`/foo/` に対するリクエストは `/foo` にリダイレクトされます。

代わりに、末尾のスラッシュが常に存在するようにしたい場合は、`trailingSlash` オプションをそれに応じて指定することができます。

```js
/// file: src/routes/always/+page.server.js
export const trailingSlash = 'always';
```

両方とも許容するには (これは推奨されません！)、`'ignore'` を使用します。

```js
/// file: src/routes/ignore/+page.server.js
export const trailingSlash = 'ignore';
```

デフォルトの値は `'never'` です。

末尾のスラッシュが適用されるかどうかは、プリレンダリングに影響します。`/always/` のような URL は、`always/index.html` としてディスクに保存され、一方で `/never` のような URL は `never.html` のように保存されます。
