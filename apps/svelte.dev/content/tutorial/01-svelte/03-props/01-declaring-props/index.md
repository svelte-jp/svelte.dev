---
title: Declaring props
---

これまで、内部状態についてのみ扱ってきました。つまり、値はそのコンポーネント内からしかアクセスできないということです。

実際のアプリケーションでは、あるコンポーネントから、その子コンポーネントにデータを渡す必要があります。そのためには、 _プロパティ(properties)_ を宣言する必要があります。通常は 'props' と省略されます。Svelteでは、`$props` rune を使用してこれを行います。`Nested.svelte` コンポーネントを編集してみましょう。

```svelte
/// file: Nested.svelte
<script>
	let { answer } = +++$props()+++;
</script>
```
