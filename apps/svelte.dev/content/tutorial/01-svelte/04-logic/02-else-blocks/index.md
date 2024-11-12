---
title: Else blocks
---

JavaScript と同じように、`if` ブロックには `else` ブロックを置くことができます:

```svelte
/// file: App.svelte
{#if count > 10}
	<p>{count} is greater than 10</p>
+++{:else}
	<p>{count} is between 0 and 10</p>+++
{/if}
```

`{#...}` はブロックを開始します。`{/...}` はブロックを終了します。`{:...}` はブロックを継続します。おめでとうございます！あなたは既にSvelteがHTMLに追加した構文のほとんどを学びました。
