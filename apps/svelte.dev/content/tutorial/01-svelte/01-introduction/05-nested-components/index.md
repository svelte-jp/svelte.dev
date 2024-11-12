---
title: Nested components
---

アプリ全体を単一のコンポーネントにまとめるのは現実的ではありません。代わりに、他のファイルからコンポーネントをインポートし、マークアップでそれを使用することができます。

`<script>` タグを `App.svelte` の上部に追加して `Nested.svelte` をインポートしましょう…

```svelte
/// file: App.svelte
+++<script>
	import Nested from './Nested.svelte';
</script>+++
```

…そして `<Nested />` コンポーネントを使用します。

```svelte
/// file: App.svelte
<p>This is a paragraph.</p>
+++<Nested />+++
```

`Nested.svelte` には `<p>` 要素がありますが、`App.svelte` のスタイルが適用されていないことに注目してください。

> [!NOTE] HTML 要素と区別するため、コンポーネントの名前は常に大文字で始まっています 
