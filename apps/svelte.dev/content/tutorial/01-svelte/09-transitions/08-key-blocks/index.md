---
title: Key blocks
---

Key ブロックは、式の値が変更されたときにその中身を破棄して再作成します。これは、要素がDOMに出入りしたときだけでなく、値が変化したときにトランジションしたい場合に便利です。

ここでは例えば、`transition.js` の `typewriter` トランジションを、ローディングメッセージが変わる度に、つまり `i` が変わる度に再生させたいと思います。`<p>` 要素を key ブロックで囲みます。

```svelte
/// file: App.svelte
+++{#key i}+++
	<p in:typewriter={{ speed: 10 }}>
		{messages[i] || ''}
	</p>
+++{/key}+++
```
