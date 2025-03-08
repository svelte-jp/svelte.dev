---
title: Stores
---

Svelte 5 でルーンが導入される前は、ストアはコンポーネント外部のリアクティブ状態を処理するための慣用的な方法でした。これはもう当てはまりませんが、Svelte (現時点では SvelteKit も含む) を使用するときにはまだストアに遭遇することになるため、その使い方を知っておくことは価値があります。

> [!NOTE] 独自のカスタム ストアを作成する方法については説明しません。その場合は、[ドキュメント](/docs/svelte/stores)を参照してください。

[ユニバーサル リアクティビティ](universal-reactivity) 演習の例をもう一度見てみましょう。ただし、今回はストアを使用して共有状態を実装します。

今 `shared.js` では、数値である `count` をエクスポートしています。これを書き込み可能なストアに変換します。

```js
/// file: shared.js
+++import { writable } from 'svelte/store';+++

export const count = +++writable(0)+++;
```

ストアの値を参照するには、先頭に `$` 記号を付けます。`Counter.svelte` で、`<button>` 内のテキストを更新して、`[object Object]` と表示されないようにします。

```svelte
/// file: Counter.svelte
<button onclick={() => {}}>
	clicks: {+++$count+++}
</button>
```

最後に、イベント ハンドラーを追加します。これは書き込み可能なストアなので、`set` または `update` メソッドを使用してプログラムで値を更新できます...

```js
count.update((n) => n + 1);
```

...ただし、コンポーネント内にいるので、`$` プレフィックスを引き続き使用できます。

```svelte
/// file: Counter.svelte
<button onclick={() => +++$count += 1+++}>
	clicks: {$count}
</button>
```
