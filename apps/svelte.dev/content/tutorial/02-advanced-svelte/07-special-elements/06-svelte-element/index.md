---
title: <svelte:element>
---

どの DOM 要素をレンダリングするのかいつも事前にわかるとはかぎりません。長い `{#if ...}` ブロックのリストを用意するよりむしろ...

```svelte
/// file: App.svelte
{#if selected === 'h1'}
	<h1>I'm a <code>&lt;h1&gt;</code> element</h1>
{:else}
	<p>TODO others</p>
{/if}
```

...`<svelte:element>` を使用したほうがよいでしょう:

```svelte
/// file: App.svelte
+++<svelte:element this={selected}>
	I'm a <code>&lt;{selected}&gt;</code> element
</svelte:element>+++
```

`this` の値は任意の文字列、または falsy な値です。falsy である場合、要素はレンダリングされません。
