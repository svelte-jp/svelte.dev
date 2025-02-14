---
NOTE: do not edit this file, it is generated in apps/svelte.dev/scripts/sync-docs/index.ts
title: <svelte:window>
---

```svelte
<svelte:window onevent={handler} />
```

```svelte
<svelte:window bind:prop={value} />
```

`<svelte:window>` 要素を使用すると、コンポーネントが破棄される際にイベントリスナーを削除する手間や、サーバーサイドレンダリング時に `window` の存在を確認する必要がなく、`window` オブジェクトにイベントリスナーを追加することができます。

この要素はコンポーネントのトップレベルにのみ配置できます — ブロックや他の要素の中に含めることはできません。

```svelte
<script>
	function handleKeydown(event) {
		alert(`pressed the ${event.key} key`);
	}
</script>

<svelte:window onkeydown={handleKeydown} />
```

以下のプロパティにもバインドできます:

- `innerWidth`
- `innerHeight`
- `outerWidth`
- `outerHeight`
- `scrollX`
- `scrollY`
- `online` — an alias for `window.navigator.onLine`
- `devicePixelRatio`

`scrollX` と `scrollY` を除くすべてのプロパティは読取専用です。

```svelte
<svelte:window bind:scrollY={y} />
```

> [!NOTE] アクセシビリティの問題を避けるため、ページは初期値にスクロールされません。`scrollX` や `scrollY` にバインドされた変数の変更があった場合のみスクロールが発生します。コンポーネントがレンダリングされたときにスクロールを発生させる正当な理由がある場合は、`$effect` 内で `scrollTo()` を呼び出してください。
