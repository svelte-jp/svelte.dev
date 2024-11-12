---
title: SvelteKit とは？
---

Svelte が _コンポーネントフレームワーク_ であるのに対し、SvelteKit は _アプリケーションフレームワーク_ であり (または、'メタフレームワーク'(metaframework) と呼ぶ人もいます)、プロダクションレディ(production-ready)なものを開発する際のややこしい問題を解決します:

- ルーティング(Routing)
- サーバーサイドレンダリング(Server-side rendering)
- データ取得(Data fetching)
- Service workers
- TypeScript インテグレーション
- プリレンダリング(Prerendering)
- シングルページアプリ(Single-page apps)
- ライブラリのパッケージング
- プロダクション向けビルドの最適化
- 様々なホスティングプロバイダーへのデプロイ
- ...などなど

SvelteKit アプリはデフォルトでは (従来の 'マルチページアプリ'、MPA のように) サーバーでレンダリングを行うため、優れた初期ロードパフォーマンスと SEO 特性を備えており、初回のロードのあとは (モダンな 'シングルページアプリ'、SPA のような) クライアントサイドナビゲーションに移行するため、ユーザーが移動する際の不愉快なフルリロードを回避することができます (サードパーティーの analytics コードを含む)。JavaScript が動作する場所ならどこでも実行できます。ただ、後ほど説明しますが、あなたのユーザーは JavaScript を実行する必要が無いかもしれません。

複雑そうに聞こえるかもしれませんが、ご心配なく。SvelteKit はあなたに合わせてくれるフレームワークです！ シンプルに始めてみて、必要に応じて新しい機能を使っていきましょう。

## プロジェクト構造 <!--Project-structure-->

右にあるファイルツリービューアには、SvelteKit のプロジェクトに含まれているであろうファイルの一部が表示されています。

Node.js を使用したことがあるなら、`package.json` はおなじみでしょう。プロジェクトの依存関係 (`svelte` と `@sveltejs/kit` を含む) と、SvelteKit CLI を操作するための様々な `scripts` がリストアップされています。(現在、このウィンドウのバックグラウンドで `npm run dev` が実行されています)

> [!NOTE] `"type": "module"` が指定されていることにもご注意ください。つまり、デフォルトで、`.js` ファイルはレガシーな CommonJS フォーマットではなくネイティブの JavaScript モジュールとして扱われます。

`svelte.config.js` にはプロジェクトの設定が記述されています。今はこのファイルについて気にする必要はありませんが、もし興味があれば、[ドキュメントを参照してください](/docs/kit/configuration)。

`vite.config.js` には [Vite](https://vitejs.dev/) の設定が含まれています。SvelteKit は Vite を使用しているので、hot module replacement (HMR) や、TypeScript サポート、静的アセットハンドリングなどの [Vite の機能](https://vitejs.dev/guide/features.html) を使うことができます。

`src` はアプリのソースコードを置く場所です。`src/app.html` はページのテンプレート (SvelteKit が `%sveltekit.head%` と `%sveltekit.body%` を適切に置き換えます) で、`src/routes` はアプリの [ルート(routes)](/tutorial/kit/pages) を定義します。

最後に、`static` にはアプリをデプロイするときに含めるべきアセット (`favicon.png` や `robots.txt` など) を置きます。
