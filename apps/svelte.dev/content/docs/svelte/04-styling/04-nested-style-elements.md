---
NOTE: do not edit this file, it is generated in apps/svelte.dev/scripts/sync-docs/index.ts
title: Nested <style> elements
---

コンポーネント1つに対しトップレベルの `<style>` タグは 1 つだけ使用できます。

しかし、他の要素やロジックブロックの内側に `<style>` タグをネストすることは可能です。

その場合、`<style>` タグはそのまま DOM に挿入され、その `<style>` タグに対するスコープの適用や処理は一切行われません。

```svelte
<div>
	<style>
		/* この <style> タグはそのまま挿入されます */
		div {
			/* これは DOM 内のすべての `<div>` 要素に適用されます */
			color: red;
		}
	</style>
</div>
```
