---
title: Shorthand class directive
---

多くの場合、クラスの名前はそれが依存する値の名前と同じになります。

```svelte
<button
	class="card"
	class:flipped={flipped}
	onclick={() => flipped = !flipped}
>
```

そのような場合は、省略形を使うことができます。

```svelte
/// file: App.svelte
<button
	class="card"
	+++class:flipped+++
	onclick={() => flipped = !flipped}
>
```
