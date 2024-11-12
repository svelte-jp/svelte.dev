---
title: ssr
---

サーバーサイドレンダリング (Server-side rendering, SSR) とはサーバーで HTML を生成するプロセスのことで、SvelteKit はデフォルトでこれを行っています。パフォーマンスと[レジリエンス](https://kryogenix.org/code/browser/everyonehasjs.html)のために重要であり、検索エンジン最適化 (SEO) にも非常に有益です。なぜなら、一部の検索エンジンではブラウザ上で JavaScript によってレンダリングされたコンテンツをインデックスできますが、その頻度は少なく、信頼性は低いためです。

一方で、サーバーでレンダリング _できない_ コンポーネントもあります。例えば、`window` のようなブラウザのグローバルにアクセスできることを想定している場合などです。もし可能なら、コンポーネントを変更してサーバーでもレンダリングできるようにしたほうが良いですが、それができない場合は、SSR を無効にすることができます。

```js
/// file: src/routes/+page.server.js
export const ssr = false;
```

> [!NOTE] 最上位(root) の `+layout.server.js` で `ssr` を `false` にすることは、実質的にはアプリ全体をシングルページアプリ (SPA) にすることになります。
