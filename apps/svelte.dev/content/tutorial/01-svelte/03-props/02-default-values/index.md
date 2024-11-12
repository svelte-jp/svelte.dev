---
title: Default values
---

`Nested.svelte` の props のデフォルト値を簡単に指定することができます。

```svelte
/// file: Nested.svelte
<script>
	let { answer +++= 'a mystery'+++ } = $props();
</script>
```

`answer` prop なしで2つ目のコンポーネントを追加すると、デフォルト値にフォールバックすることがわかります。

```svelte
/// file: App.svelte
<Nested answer={42}/>
+++<Nested />+++
```
