---
title: Exports
---

`module` スクリプトブロックからエクスポートされたものはすべてモジュール自体からのエクスポートになります。`stopAll` 関数をエクスポートしましょう:

```svelte
/// file: AudioPlayer.svelte
<script module>
	let current;

+++	export function stopAll() {
		current?.pause();
	}+++
</script>
```

`App.svelte` で `stopAll` をインポートすることができます…

```svelte
/// file: App.svelte
<script>
	import AudioPlayer, +++{ stopAll }+++ from './AudioPlayer.svelte';
	import { tracks } from './tracks.js';
</script>
```

…さらにそれをイベントハンドラで使うことができます。

```svelte
/// file: App.svelte
<div class="centered">
	{#each tracks as track}
		<AudioPlayer {...track} />
	{/each}

+++	<button onclick={stopAll}>
		stop all
	</button>+++
</div>
```

> [!NOTE] default export は使うことはできません、なぜならコンポーネント自体が default export だからです。
