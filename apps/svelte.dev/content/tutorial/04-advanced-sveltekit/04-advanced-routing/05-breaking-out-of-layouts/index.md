---
title: Breaking out of layouts
editing_constraints:
  { 'create': ['/src/routes/a/b/c/+page@b.svelte', '/src/routes/a/b/c/+page@a.svelte'] }
---

通常、ページはその上にある全てのレイアウトを継承しています。つまり、`src/routes/a/b/c/+page.svelte` は4つのレイアウトを継承しています。

- `src/routes/+layout.svelte`
- `src/routes/a/+layout.svelte`
- `src/routes/a/b/+layout.svelte`
- `src/routes/a/b/c/+layout.svelte`

たまに、現在のレイアウト階層から抜け出せると便利なときもあります。`@` 記号の後に'リセット'する親セグメントの名前を追加することで、これを実現することができます — 例えば、`/a/b/c` で `+page@b.svelte` にすると `src/routes/a/b/+layout.svelte` が適用され、`+page@a.svelte` の場合は `src/routes/a/+layout.svelte` が適用されます。

`+page@.svelte` にリネームして、一気に最上位(root)のレイアウトまでリセットしてみましょう。

> [!NOTE] 最上位(root)のレイアウトはアプリの全てのページに適用され、そこから抜け出すことはできません。
