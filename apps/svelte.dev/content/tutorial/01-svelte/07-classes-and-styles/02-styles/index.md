---
title: The style directive
---

`class` と同じように、`style` 属性を文字通りインラインで書くことができます。なぜなら Svelte は、実際にはちょっと素敵なものを加えただけの HTML だからです:

```svelte
/// file: App.svelte
<button
	class="card"
	+++style="transform: {flipped ? 'rotateY(0)' : ''}; --bg-1: palegoldenrod; --bg-2: black; --bg-3: goldenrod"+++
	onclick={() => flipped = !flipped}
>
```

style がたくさんあるときは少し散らかって見えるかもしれません。`style:` ディレクティブを使用して整理することができます:

```svelte
/// file: App.svelte
<button
	class="card"
+++	style:transform={flipped ? 'rotateY(0)' : ''}
	style:--bg-1="palegoldenrod"
	style:--bg-2="black"
	style:--bg-3="goldenrod"+++
	onclick={() => flipped = !flipped}
>
```
