---
NOTE: do not edit this file, it is generated in apps/svelte.dev/scripts/sync-docs/index.ts
title: sv add
---

`sv add`は、既存のプロジェクトに新しい機能を追加するコマンドです。

## 使用方法 <!--Usage-->

```bash
npx sv add
```

```bash
npx sv add [add-ons]
```

スペースで区切った複数のアドオンを[以下のリスト](#Official-add-ons)から選択するか、対話型プロンプトを使用することができます。

## オプション <!--Options-->

- `-C`, `--cwd` — Svelte(Kit)プロジェクトのルートへのパス
- `--no-preconditions` — 前提条件の確認をスキップ <!-- TODO what does this mean? -->
- `--install` — パッケージマネージャーを指定して依存関係(dependencies) のインストールを行う
- `--no-install` — 依存関係のインストールを行わない

## 公式アドオン <!--Official-add-ons-->

<!-- TODO: it'd be nice for this to live on the "add-ons" page, but we first need svelte.dev to support making pages from headings -->

- [`drizzle`](drizzle)
- [`eslint`](eslint)
- [`lucia`](lucia)
- [`mdsvex`](mdsvex)
- [`paraglide`](paraglide)
- [`playwright`](playwright)
- [`prettier`](prettier)
- [`storybook`](storybook)
- [`sveltekit-adapter`](sveltekit-adapter)
- [`tailwindcss`](tailwind)
- [`vitest`](vitest)
