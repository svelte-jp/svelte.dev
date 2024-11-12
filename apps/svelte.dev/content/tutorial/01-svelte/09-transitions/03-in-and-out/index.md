---
title: In and out
---

`transition` ディレクティブの代わりに、要素に `in` や `out`、または両方のディレクティブを設定することができます。`fly` と一緒に `fade` をインポートしてください。

```js
/// file: App.svelte
import { +++fade+++, fly } from 'svelte/transition';
```

その後、`transition` ディレクティブを `in` と `out` ディレクティブにそれぞれ置き換えてください。

```svelte
/// file: App.svelte
<p +++in+++:fly={{ y: 200, duration: 2000 }} +++out:fade+++>
	Flies in, +++fades out+++
</p>
```

この場合、トランジションは可逆的にはなりません。
