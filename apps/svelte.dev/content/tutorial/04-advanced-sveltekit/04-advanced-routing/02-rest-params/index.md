---
title: Rest parameters
path: /how
focus: /src/routes/[path]/+page.svelte
---

未知の数のパスセグメントにマッチさせるには、`[...rest]` パラメータを使用します。これは、 [JavaScript の残余引数(rest parameters)](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Functions/rest_parameters) に似ているため、この名前が付けられました。

`src/routes/[path]` を `src/routes/[...path]` にリネームしましょう。このルート(route)はどんなパスにもマッチします。

> [!NOTE] 他の、より詳細・明確(specific)なルート(routes)が最初にテストされるため、rest パラメータは 'catch-all' ルート(routes)として便利です。例えば、`/categories/...` の中のページ用にカスタムの 404 ページを必要とする場合は、以下のファイルを追加することができます。
>
> ```tree
> src/routes/
> ├ categories/
> │ ├ animal/
> │ ├ mineral/
> │ ├ vegetable/
> +++│ ├ [...catchall]/
> │ │ ├ +error.svelte
> │ │ └ +page.server.js+++
> ```
>
> `+page.server.js` ファイルにて、`load` の内側で `error(404)` のようにエラーをスローします。

Rest parameters はパスの末尾にしなければならないわけではありません。 — `/items/[...path]/edit` や `/items/[...path].json` のようなルート(route)は完全に有効です。
