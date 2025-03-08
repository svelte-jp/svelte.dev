---
title: Raw state
---

前回の演習では、状態が [深く反応する](deep-state) ことを学びました。つまり、(たとえば) オブジェクトのプロパティを変更したり、配列にプッシュしたりすると、UI が更新されます。これは、読み取りと書き込みをインターセプトする [プロキシ](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Proxy) を作成することで機能します。

場合によっては、それが望ましくないこともあります。個々のプロパティを変更しない場合、または参照の等価性を維持することが重要である場合は、代わりに _raw state_ を使用できます。

この例では、Svelte の株価が着実に上昇しているグラフがあります。新しいデータが入ったときにグラフを更新したいのですが、これは `data` を state に変換することで実現できます...

```js
/// file: App.svelte
let data = +++$state(poll())+++;
```

...しかし、数ミリ秒後に破棄されるのであれば、それを深く反応させる必要はありません。代わりに、`$state.raw` を使用します。

```js
/// file: App.svelte
let data = +++$state.raw(poll())+++;
```

> [!NOTE] _raw state_ を変更してもエフェクトは反応しません。一般に非反応状態を変更することは強く推奨されません。
