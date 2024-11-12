---
title: Spread props
---

この演習では、`PackageInfo.svelte` が期待する `name` prop を指定し忘れているため、`<code>` 要素が空になり、npm link が壊れています。

以下のように prop を追加することで、これを修正できます…

```svelte
/// file: App.svelte
<PackageInfo
	+++name={pkg.name}+++
	version={pkg.version}
	description={pkg.description}
	website={pkg.website}
/>
```

…ただ、`pkg` のプロパティはこのコンポーネントが期待する props と一致しているので、代わりに 'spread' 構文を使用することができます:

```svelte
/// file: App.svelte
<PackageInfo +++{...pkg}+++ />
```

> [!NOTE] 逆に、rest プロパティを使用して、そのコンポーネントに渡されたオブジェクトの props を全て受け取ることができます...
>
> ```js
> let { name, ...stuff } = $props();
> ```
>
> ...もしくは、[destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) を完全にスキップします:
>
> ```js
> let stuff = $props();
> ```
