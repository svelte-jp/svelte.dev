---
NOTE: do not edit this file, it is generated in apps/svelte.dev/scripts/sync-docs/index.ts
title: <svelte:boundary>
---

```svelte
<svelte:boundary onerror={handler}>...</svelte:boundary>
```

> [!NOTE]
> この機能は 5.3.0 で追加されました

boundary (境界) を使用すると、アプリの一部で発生したエラーがアプリ全体を壊すのを防ぎ、それらのエラーから回復することができます。

`<svelte:boundary>` 内の子要素をレンダリングまたは更新するとき、あるいはそれに含まれる [`$effect`]($effect) 関数の実行中にエラーが発生すると、そのコンテンツは削除されます。

レンダリングプロセスの外で発生するエラー (例えば、イベントハンドラー内で発生するエラーや、`setTimeout`や非同期処理の後のエラー) は error boundary では捕捉されません。

## プロパティ <!--Properties-->

boundary を機能させるには、`failed` または `onerror` のいずれか、または両方を提供する必要があります。

### `failed`

`failed` snippet が提供されると、スローされた error と、コンテンツを再作成する `reset` 関数を引数に取ってレンダリングされます ([デモ](/playground/hello-world#H4sIAAAAAAAAE3VRy26DMBD8lS2tFCIh6JkAUlWp39Cq9EBg06CAbdlLArL87zWGKk8ORnhmd3ZnrD1WtOjFXqKO2BDGW96xqpBD5gXerm5QefG39mgQY9EIWHxueRMinLosti0UPsJLzggZKTeilLWgLGc51a3gkuCjKQ7DO7cXZotgJ3kLqzC6hmex1SZnSXTWYHcrj8LJjWTk0PHoZ8VqIdCOKayPykcpuQxAokJaG1dGybYj4gw4K5u6PKTasSbjXKgnIDlA8VvUdo-pzonraBY2bsH7HAl78mKSHZpgIcuHjq9jXSpZSLixRlveKYQUXhQVhL6GPobXAAb7BbNeyvNUs4qfRg3OnELLj5hqH9eQZqCnoBwR9lYcQxuVXeBzc8kMF8yXY4yNJ5oGiUzP_aaf_waTRGJib5_Ad3P_vbCuaYxzeNpbU0eUMPAOKh7Yw1YErgtoXyuYlPLzc10_xo_5A91zkQL_AgAA)):

```svelte
<svelte:boundary>
	<FlakyComponent />

	{#snippet failed(error, reset)}
		<button onclick={reset}>oops! try again</button>
	{/snippet}
</svelte:boundary>
```

> [!NOTE]
> [コンポーネントに渡される snippet](snippet#Passing-snippets-to-components) と同様に、`failed` snippet はプロパティとして明示的に渡すことができます...
>
> ```svelte
> <svelte:boundary {failed}>...</svelte:boundary>
> ```
>
> ...または、上記の例のように boundary 内に直接記述することで暗黙的に渡すこともできます。

### `onerror`

`onerror` 関数が提供されると、`failed` と同じ `error` と `reset` の2つの引数とともに呼び出されます。これはエラーレポートサービスでエラーを追跡するのに役立ちます...

```svelte
<svelte:boundary onerror={(e) => report(e)}>
	...
</svelte:boundary>
```

...または、`error` と `reset` を boundary の外部で使用することもできます:

```svelte
<script>
	let error = $state(null);
	let reset = $state(() => {});

	function onerror(e, r) {
		error = e;
		reset = r;
	}
</script>

<svelte:boundary {onerror}>
	<FlakyComponent />
</svelte:boundary>

{#if error}
	<button onclick={() => {
		error = null;
		reset();
	}}>
		oops! try again
	</button>
{/if}
```

`onerror` 関数内でエラーが発生した場合 (またはエラーを再スローした場合)、もし親の boundary が存在すればそこで処理されます。
