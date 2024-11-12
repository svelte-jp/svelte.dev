---
title: Preloading
---

この演習では、`/slow-a` と `/slow-b` の両方のルートにわざと遅延を設けています (`load` 関数でそれを行っています)。つまり、そこに移動しようとすると時間がかかるようになっています。

データの読み込みをいつも速くできるとは限りません — コントロールできないこともあります — しかし、SvelteKit は事前読み込みをすることで、ナビゲーションを高速化することができます。`<a>` 要素に `data-sveltekit-preload-data` 属性を付けると、デスクトップの場合はリンクをホバーしたとき、モバイルの場合はリンクをタップしたとき、すぐにナビゲーションを開始します。これをリンクに付けてみましょう:

```svelte
/// file: src/routes/+layout.svelte
<nav>
	<a href="/">home</a>
	<a href="/slow-a" +++data-sveltekit-preload-data+++>slow-a</a>
	<a href="/slow-b">slow-b</a>
</nav>
```

`/slow-a` へのナビゲーションが格段に速くなるはずです。`click` イベントの登録を待つのではなく、ホバーやタップでナビゲーションで開始するのは、あまり違いがないように聞こえるかもしれませんが、実際には、通常 200ms 以上短縮することができ、遅いか速いか違いを感じるのに十分な差となります。

この属性は、個々のリンクに付けることもできますし、リンクを含む任意の要素に付けることもできます。デフォルトのプロジェクトテンプレートでは、`<body>` 要素に付いています:

```html
<body data-sveltekit-preload-data>
	%sveltekit.body%
</body>
```

この属性に以下の値のいずれかを指定すると、この動作をさらにカスタマイズすることができます:

- `"hover"` (デフォルト。モバイルでは `"tap"` にフォールバックする)
- `"tap"` — タップしたときのみプリロードを開始する
- `"off"` — プリロードを無効にする

`data-sveltekit-preload-data` を使用すると、偽陽性(false positives)になることがあります。つまり、ナビゲーションを先読みしてデータを読み込むもののそのあと実際にはナビゲーションしないことがあり、それが望ましくない場合もあるということです。代わりに `data-sveltekit-preload-code` を使用すると、データを読み込むことなくそのルートに必要な JavaScript をプリロードすることができます。この属性は以下の値を持つことができます:

- `"eager"` — ナビゲーションに続いてページ上の全てをプリロードする
- `"viewport"` — viewport に表示されているものを全てプリロードする
- `"hover"` (デフォルト) 上記の通り
- `"tap"` — 上記の通り
- `"off"` — 上記の通り

`$app/navigation` からインポートできる `preloadCode` と `preloadData` を使うと、プログラムでプリロードを開始することができます:

```js
import { preloadCode, preloadData } from '$app/navigation';

// preload the code and data needed to navigate to /foo
preloadData('/foo');

// preload the code needed to navigate to /bar, but not the data
preloadCode('/bar');
```
