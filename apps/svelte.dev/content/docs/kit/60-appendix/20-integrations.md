---
NOTE: do not edit this file, it is generated in apps/svelte.dev/scripts/sync-docs/index.ts
title: Integrations
---

## `vitePreprocess`

プロジェクトに [`vitePreprocess`](https://github.com/sveltejs/vite-plugin-svelte/blob/main/docs/preprocess.md) を含めることで、Vite がサポートする様々な CSS のフレーバー (PostCSS、SCSS、Less、Stylus、SugarSS) を使用することができます。プロジェクトを TypeScript でセットアップすると、TypeScript はデフォルトで含まれるようになります:

```js
// svelte.config.js
import { vitePreprocess } from '@sveltejs/vite-plugin-svelte';

export default {
  preprocess: [vitePreprocess()]
};
```

You will also need to use a preprocessor if you're using TypeScript with Svelte 4. TypeScript is supported natively in Svelte 5 if you're using only the type syntax. To use more complex TypeScript syntax in Svelte 5, you will need still need a preprocessor and can use `vitePreprocess({ script: true })`.

## Adders

`npx sv add` によって、様々な複雑なインテグレーションを単一のコマンドでセットアップすることができます:
- prettier (formatting)
- eslint (linting)
- vitest (unit testing)
- playwright (e2e testing)
- lucia (auth)
- tailwind (CSS)
- drizzle (DB)
- paraglide (i18n)
- mdsvex (markdown)
- storybook (frontend workshop)

## Directory

Svelte と SvelteKit で使用できる [パッケージ](https://sveltesociety.dev/packages) や [テンプレート](https://sveltesociety.dev/templates) のリストは [sveltesociety.dev](https://sveltesociety.dev/) でご覧いただけます。

## Additional integrations

### `svelte-preprocess`

`svelte-preprocess` は、Pug、Babel、global styles のサポートなど、`vitePreprocess` には無い機能があります。しかし、`vitePreprocess` はより速く、設定が少ないため、デフォルトでは `vitePreprocess` が使用されます。SvelteKit は CoffeeScript を [サポートしていない](https://github.com/sveltejs/kit/issues/2920#issuecomment-996469815) ことにご注意ください。

`svelte-preprocess` をインストールするには `npm install --save-dev svelte-preprocess` を実行し、ご自身で [`svelte.config.js` に追加する](https://github.com/sveltejs/svelte-preprocess/blob/main/docs/usage.md#with-svelte-config) 必要があります。その後、`npm install -D sass` や `npm install -D less` など、[対応するライブラリのインストール](https://github.com/sveltejs/svelte-preprocess/blob/main/docs/getting-started.md) が必要になることが多いようです。

## Vite plugins

SvelteKit プロジェクトは Vite で構築されているため、Vite plugin を使用してプロジェクトを拡張することができます。利用可能な plugin のリストは [`vitejs/awesome-vite`](https://github.com/vitejs/awesome-vite?tab=readme-ov-file#plugins) をご覧ください。

## Integration FAQs

[SvelteKit FAQ](./faq) にて、SvelteKit で X をする方法に関する多くの質問に対する回答があるので、、もしまだ不明点があるようでしたら役に立つかもしれません。
