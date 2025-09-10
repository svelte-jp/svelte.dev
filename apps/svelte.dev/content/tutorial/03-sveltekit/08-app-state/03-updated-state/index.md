---
title: updated
---

`updated` state は `true` または `false` を持ちます。これは最初にページを開いてからそれ以降にアプリの新バージョンがデプロイされたかどうかを表しています。これを動作させるには、`svelte.config.js` で `kit.version.pollInterval` を指定する必要があります。

```svelte
/// file: src/routes/+layout.svelte
<script>
	import { page, navigating, +++updated+++ } from '$app/state';
</script>
```

バージョンの変更はプロダクションでのみ発生し、開発時には発生しません。そのため、このチュートリアルでは `updated.current` は常に `false` となります。

`pollInterval` とは関係なく、`updated.check()` を呼び出すと手動で新バージョンがデプロイされたかチェックできます。

```svelte
/// file: src/routes/+layout.svelte

+++{#if updated.current}+++
	<div class="toast">
		<p>
			A new version of the app is available

			<button onclick={() => location.reload()}>
				reload the page
			</button>
		</p>
	</div>
+++{/if}+++
```

> [!NOTE] SvelteKit 2.12より前は、`$app/stores` が提供する `$updated` storeが同じ役割を担っていました。いま `$app/stores` を使っている場合は、 `$app/state` への移行をおすすめします。(Svelte 5が必要です。)
