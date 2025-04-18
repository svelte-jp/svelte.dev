---
NOTE: do not edit this file, it is generated in apps/svelte.dev/scripts/sync-docs/index.ts
title: <svelte:document>
---

```svelte
<svelte:document onevent={handler} />
```

```svelte
<svelte:document bind:prop={value} />
```

`<svelte:window>` と似ていますが、この要素を使用すると `window` では発火しない `visibilitychange` などの `document` のイベントにリスナーを追加できます。また、`document` に対して [action](use) を使用することも可能です。

`<svelte:window>` と同様に、この要素はコンポーネントのトップレベルにのみ配置でき、ブロックや他の要素の中に含めることはできません。

```svelte
<svelte:document onvisibilitychange={handleVisibilityChange} use:someAction />
```

以下のプロパティにもバインドできます:

- `activeElement`
- `fullscreenElement`
- `pointerLockElement`
- `visibilityState`

すべて読取専用です。
