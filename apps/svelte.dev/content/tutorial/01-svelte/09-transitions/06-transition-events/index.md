---
title: Transition events
---

トランジションの開始と終了のタイミングを知ることができれば便利です。Svelteは、他のDOMイベントと同じようにリッスンすることができるイベントをディスパッチします。

```svelte
/// file: App.svelte
<p
	transition:fly={{ y: 200, duration: 2000 }}
+++	onintrostart={() => status = 'intro started'}
	onoutrostart={() => status = 'outro started'}
	onintroend={() => status = 'intro ended'}
	onoutroend={() => status = 'outro ended'}+++
>
	Flies in and out
</p>
```
