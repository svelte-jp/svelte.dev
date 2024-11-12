---
title: "What's new in Svelte: 2022年2月"
description: "Svelte、SvelteKit、コミュニティを横断し、畳み掛けるようにリリース"
author: Dani Sandoval
authorURL: https://dreamindani.com
---

Happy February, everyone! ここ1か月ほどで、Svelte と SvelteKit の [開発が加速し](accelerating-sveltes-development)、[Reddit](https://www.reddit.com/r/sveltejs/comments/s9n8ou/new_rules/)、[GitHub](https://github.com/sveltejs/community/blob/main/CODE_OF_CONDUCT.md)、[Discord](https://discord.com/channels/457912077277855764/831611707667382303/935264550436102315) で新しいコミュニティのルールができ、そしてかなりの数の素晴らしいアプリ、チュートリアル、ライブラリがリリースされました。

それでは見ていきましょう…

## Highlights from the Svelte changelog

- **3.45.0** brought a [new a11y warning `a11y-no-redundant-roles`](https://v4.svelte.dev/docs#accessibility-warnings-a11y-no-redundant-roles), destructuring and caching fixes
- **3.46.0** added the much requested [`{@const}` tag](https://v4.svelte.dev/docs#template-syntax-const) and [`style:` directive](https://v4.svelte.dev/docs#template-syntax-element-directives-style-property)
- Check out **3.46.1 - 3.46.3** for fixes to the `{@const}` tag and `style:` directive, along with a number of fixes to animations
- [AST output is now available in the Svelte REPL](/playground/hello-world)

## What's new in SvelteKit

- `inlineStyleThreshold` allows you to specify where inline stylesheets are inserted into the page ([Docs](/docs/kit/configuration#inlineStyleThreshold), [#2620](https://github.com/sveltejs/kit/pull/2620))
- `beforeNavigate`/`afterNavigate` lifecycle functions lets you add functionality before or after a page navigation ([Docs](/docs/kit/$app-navigation), [#3293](https://github.com/sveltejs/kit/pull/3293))
- Platform context can now be passed from adapters ([Docs](/docs/kit/adapters#Platform-specific-context), [#3429](https://github.com/sveltejs/kit/pull/3429))
- Hooks now have an `ssr` parameter in `resolve` to make it easier to skip SSR, when needed ([Docs](/docs/kit/hooks#Server-hooks-handle), [#2804](https://github.com/sveltejs/kit/pull/2804))
- `$page.stuff` provides a mechanism for pages to pass data 'upward' to layouts ([Docs](https://kit.svelte.dev/docs/loading#input-stuff), [#3252](https://github.com/sveltejs/kit/pull/3252))
- Fallthrough routes let you specify where to route when an route can't be loaded ([#3217](https://github.com/sveltejs/kit/pull/3217))

### New configs

- Content Security Policy (CSP) is now supported for increased security when using inline javascript or stylesheets ([Docs](/docs/kit/configuration#csp), [#3499](https://github.com/sveltejs/kit/pull/3499))
- `kit.routes` config allows you to customise public/private modules during build ([#3576](https://github.com/sveltejs/kit/pull/3576))
- `prerender.createIndexFiles` config lets you prerender index.html files as their subfolder's name ([#2632](https://github.com/sveltejs/kit/pull/2632))
- HTTP methods can now be overridden using `kit.methodOverride` ([Docs](https://kit.svelte.dev/docs/routing#endpoints-http-method-overrides), [#2989](https://github.com/sveltejs/kit/pull/2989))

### Config changes

- `config.kit.hydrate` and `config.kit.router` are now nested under `config.kit.browser` ([3578](https://github.com/sveltejs/kit/pull/3578))

### Breaking change

- エンドポイント(endpoints) と Hooks で、`Request` オブジェクトと `Response` オブジェクト が使われるようになりました ([#3384](https://github.com/sveltejs/kit/pull/3384))

---

## Community Showcase

### Apps & Sites

- [timb(re)](https://paullj.github.io/timb) は、ライブミュージックプログラミング環境です
- [Music for Programming](https://musicforprogramming.net/latest/) は、`${task}` 中に聴くことで脳を集中させやる気を起こすことを目的としてミックスシリーズです
- [Team Tale](https://teamtale.app/) は、1つのストーリーを2人の執筆者がタッグを組むような形で書くことができます
- [Puzzlez](https://www.puzzlez.io/) は、数独と Wordle をオンラインでプレイできます
- [Closed Caption Creator](https://www.closedcaptioncreator.com/) は、Windows、Mac、Google Chrome で、あなたのビデオに簡単に字幕を付けられます
- [SC3Lab](https://sc3-lab.netlify.app/) は、svelte-cubed and three.js を使用した実験的なコードジェネレーターです
- [Donkeytype](https://github.com/0ql/Donkeytype) は、Monkeytype にインスパイアされた、ミニマルで軽量なタイピングテストです
- [Above](https://above.silas.pro/) は、ADHD/自閉症の方のために作られたビジュアル・ルーティーン・タイマーです
- [base.report](https://base.report/) は、本格的な投資家向けのモダンなリサーチプラットフォームです
- [String](https://string.kampsy.xyz/) は、あなたのスマートフォンをセキュアでポータブルなオーディオレコーダーに変身させ、個人的なメモ、家族の思い出、講義などを記録して共有するのを簡単にしてくれます
- [The Raytracer Challenge REPL](https://github.com/jakobwesthoff/the_raytracer_challenge_repl) は、シーンのレイトレーシングを設定してそれをレンダリングするライブ・エディター・インタフェースで、モダンなブラウザで動作します
- [awesome-svelte-kit](https://github.com/janosh/awesome-svelte-kit) は、SvelteKit の素晴らしい example のリストです
- [Map Projection Explorer](https://www.geo-projections.com/) は、様々な地図の投影法を調べ、その違いを明白にすることができます
- [Rubiks](https://github.com/MeharGaur/rubiks) はルービックキューブのシミュレーターです 
- [Pianisto](https://pianisto.net/) は、SVG と ToneJS と多くの忍耐によって作られた、実際に動くピアノです

みんなで SvelteKit サイト に取り組んでみたいなら、[Svelte Society のサイトへのコントリビュートにトライしてみてください](https://github.com/svelte-society/sveltesociety-2021/issues)!

### Learning and Listening

_To Read_

- [Accelerating Svelte's Development](/blog/accelerating-sveltes-development) by Ben McCann
- [Storybook for Vite](https://storybook.js.org/blog/storybook-for-vite/)
- [Let's learn SvelteKit by building a static Markdown blog from scratch](https://joshcollinsworth.com/blog/build-static-sveltekit-markdown-blog) by Josh Collinsworth
- [Building an iOS app with Svelte, Capacitor and Firebase](https://harryherskowitz.com/2022/01/05/tapedrop-app.html) by Harry Herskowitz
- [Mutating Query Params in SvelteKit Without Page Reloads or Navigations](https://dev.to/mohamadharith/mutating-query-params-in-sveltekit-without-page-reloads-or-navigations-2i2b) and [Workaround for Bubbling Custom Events in Svelte](https://dev.to/mohamadharith/workaround-for-bubbling-custom-events-in-svelte-3khk) by Mohamad Harith
- [How to build a full stack serverless application with Svelte and GraphQL](https://dev.to/shadid12/how-to-build-a-full-stack-serverless-application-with-svelte-graphql-and-fauna-5427) by Shadid Haque
- [How to Deploy SvelteKit Apps to GitHub Pages](https://sveltesaas.com/articles/sveltekit-github-pages-guide/)
- [Creating a dApp with SvelteKit](https://anthonyriley.org/2021/12/31/creating-a-dapp-with-sveltekit/) by Anthony Riley
- [Comparing Svelte Reactivity Options](https://opendirective.net/2022/01/06/comparing-svelte-reactivity-options/) by Steve Lee

_To Watch_

- [Integrating Storybook with SvelteKit](https://www.youtube.com/watch?v=Kc1ULlfyUcw) and [Integrating FaunaDB with Svelte](https://www.youtube.com/watch?v=zaoLZc76uZM) by the Svelte Sirens
- [SvelteKit Crash Course Tutorial](https://www.youtube.com/watch?v=9OlLxkaeVvw&list=PL4cUxeGkcC9hpM9ARM59Ve3jqcb54dqiP) by The Net Ninja
- [Svelte for Beginners](https://www.youtube.com/watch?v=BrkrOjknC_E&list=PLA9WiRZ-IS_ylnMYxIFCsZN6xVVSvLuHk) by Joy of Code
- [SvelteKit For Beginners | Movie App Tutorial](https://www.youtube.com/watch?v=ydR_M0fw9Xc) by Dev Ed
- [SvelteKit $app/stores](https://www.youtube.com/watch?v=gBPhr1xbgaQ) by lihautan
- [Sveltekit - Get All Routes/Pages](https://www.youtube.com/watch?v=Y_NE2R3HuOU) by WebJeda

_To Listen To_

- [New Year, New Svelte!?](https://share.transistor.fm/s/36212cdc) from Svelte Radio
- [So much Sveltey goodness (featuring Rich Harris)](https://changelog.com/jsparty/205) from JS Party
- [The Other Side of Tech: A Documentarian Perspective (with Stefan Kingham)](https://codingcat.dev/podcast/2-4-the-other-side-of-tech-a-documentarian-perspective) from Purrfect.dev

### Libraries, Tools & Components

- [threlte](https://github.com/grischaerbe/threlte) は Svelte 向けの three.js コンポーネントライブラリ
- [svelte-formify](https://github.com/nodify-at/svelte-formify) は、フォームの管理とバリデーションを行うライブラリで、デコレーターを使用してバリデーションを定義します
- [gQuery](https://github.com/leveluptuts/gQuery) は、SvelteKit 向けの GraphQL Fetcher & Cache です
- [Unlock-protocol](https://github.com/novum-insights/sveltekit-unlock-firebase) は、MetaMask、Firebase、paywall のユーザーのログインを支援するインテグレーションです
- [AgnosticUI](https://github.com/AgnosticUI/agnosticui) は、クリーンな HTML と CSS で構成されている UI プリミティブのセットです
- [Vitebook](https://github.com/vitebook/vitebook) は、高速で軽量な Storybook の代替で、Vite を使用しています
- [SwyxKit](https://swyxkit.netlify.app/) は、SvelteKit + Tailwind + Netlify を使用したオピニオネイテッドなブログ・スターターです。2022年に向け新しくなりました！
- [svelte-themes](https://github.com/beynar/svelte-themes) は、SvelteKit アプリのテーマを抽象化したものです
- [svelte-transition](https://www.npmjs.com/package/svelte-transition) は、CSS クラスベースのトランジションを簡単にする Svelte コンポーネントです - TailwindCSS と一緒に使用するのが望ましいです
- [Svelte Inview](https://www.npmjs.com/package/svelte-inview) は、viewport/親要素 への要素の出入りを監視する Svelte アクションです
- [svelte-inline-compile](https://github.com/DockYard/svelte-inline-compile) は、Jest と `@testing-library/svelte` を使って Svelte コンポーネントをテストする際に、より快適な体験を得るための Babel transform です
- [@feltcoop/svelte-mutable-store](https://github.com/feltcoop/svelte-mutable-store) は、`immutable` コンパイラオプションでもミュータブルな値を扱える Svelte ストアです
- [headless-svelte-ui](https://www.npmjs.com/package/@bojalelabs/headless-svelte-ui) は、Svelte アプリを構築する際に使用できるヘッドレスコンポーネント(headless components)集です

なにか見落としがありましたか？Svelte でアイデアを実現するのに助けが必要ですか？ [Reddit](https://www.reddit.com/r/sveltejs/) または [Discord](https://discord.com/invite/yy75DKs) にご参加ください。

また来月お会いしましょう！
