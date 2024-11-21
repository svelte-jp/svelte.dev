---
title: Getting started
---

Svelte チームによるオフィシャルなアプリケーションフレームワークである [SvelteKit](../kit) をお使いいただくことをおすすめします。これには [Vite](https://vite.dev/) が搭載されています:

```bash
npx sv create myapp
cd myapp
npm install
npm run dev
```

まだ Svelte についてよく知らなくても心配いりません! SvelteKit が提供する便利な機能等は一旦無視して、後から学び始めても問題ありません。

## SvelteKit の代替手段 <!--Alternatives-to-SvelteKit-->

Svelteを直接Viteで使用することもできます。その場合、`npm create vite@latest` を実行し、`svelte` オプションを選択します。この方法では、`npm run build` を実行すると、[vite-plugin-svelte](https://github.com/sveltejs/vite-plugin-svelte) を使用して、`dist` ディレクトリ内に HTML、JS、CSSファイルが生成されます。ほとんどの場合、[ルーティングライブラリ](faq#Is-there-a-router)を選択する必要があるでしょう。

また、[Rollup](https://github.com/sveltejs/rollup-plugin-svelte)、[Webpack](https://github.com/sveltejs/svelte-loader)、[その他いくつかのプラグイン](https://sveltesociety.dev/packages?category=build-plugins)もありますが、Viteをお勧めします。

## エディタツール <!--Editor-tooling-->

Svelteチームは、[VS Code 拡張機能](https://marketplace.visualstudio.com/items?itemName=svelte.svelte-vscode)を提供しています。また、様々な[他のエディター](https://sveltesociety.dev/resources#editor-support)やツールとの統合も利用可能です。

さらに、[sv check](https://github.com/sveltejs/cli) を使ってコマンドラインからコードをチェックすることもできます。

## サポートを受ける <!--Getting-help-->

[Discord チャットルーム](/chat)で気軽に質問してください！また、[Stack Overflow](https://stackoverflow.com/questions/tagged/svelte) でも回答を見つけることができます。
