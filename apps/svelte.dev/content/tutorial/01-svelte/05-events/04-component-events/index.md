---
title: Component events
---

他のプロパティと同様に、イベント ハンドラーをコンポーネントに渡すことができます。`Stepper.svelte` で、`increment` および `decrement` プロパティを追加します...

```svelte
/// file: Stepper.svelte
<script>
	let +++{ increment, decrement }+++ = $props();
</script>
```

...そしてこのように接続します。:

```svelte
/// file: Stepper.svelte
<button +++onclick={decrement}+++>-1</button>
<button +++onclick={increment}+++>+1</button>
```

`App.svelte` 内で、ハンドラーの内容を定義します。

```svelte
/// file: App.svelte
<Stepper
	+++increment={() => value += 1}+++
	+++decrement={() => value -= 1}+++
/>
```
