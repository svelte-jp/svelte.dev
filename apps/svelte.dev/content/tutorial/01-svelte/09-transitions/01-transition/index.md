---
title: The transition directive
---

要素を DOM に優美に追加したり削除したりすることで、より魅力的なユーザーインターフェイスを作成できます。Svelte は `transition` ディレクティブを使用してこれを非常に簡単にします。

まず、`svelte/transition` から `fade` 関数をインポートします。

```svelte
/// file: App.svelte
<script>
	+++import { fade } from 'svelte/transition';+++

	let visible = $state(true);
</script>
```

次に、それを `<p>` 要素に追加します。

```svelte
/// file: App.svelte
<p +++transition:fade+++>
	Fades in and out
</p>
```
