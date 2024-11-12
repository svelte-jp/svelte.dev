---
title: "What's new in Svelte: 2023年4月"
description: "たくさんの Svelte コンパイラの新機能, そして Svelte Summit と SvelteHack"
author: Dani Sandoval
authorURL: https://dreamindani.com
---

Happy April、みなさん！ 今月は、Svelte コンパイラの全ての新機能や、SvelteKit における QOL の改善、そしてたくさんのショーケースを見ていきますよ (いつものようにね)。

コアチームのニュースとしては、Dominic Gannaway が Vercel にジョインし、フルタイムで Svelte に取り組むことになりました！ Dominic は javascript エンジンのパフォーマンスや、DOM、リアクティビティ、アクセシビリティなどのワールドクラスのエキスパートです！ UI フレームワークの [Inferno](https://www.infernojs.org/) や Meta の WYSIWYG エディタである [Lexical](https://lexical.dev/) の作者としても知られています。彼の才能が Svelte エコシステムで発揮されたら、とても素晴らしい未来が待っているでしょう🌱

こちらもお忘れなく！ 6回目 となる Svelte のバーチャルカンファレンス、Svelte Summit Spring が 5月6日に開催されます。また、[SvelteHack](https://hack.sveltesociety.dev/) の締め切りまであと2週間です… あなたの作品をコミュニティにシェアする素晴らしい機会ですし、もしかしたら賞品を獲得できるかも！

それでは、今月の更新を見ていきましょう…

## What's new in Svelte

- A bunch of new features are now available as of **3.56.0**!
  - Add `|stopImmediatePropagation` event modifier for `on:eventname` ([#5085](https://github.com/sveltejs/svelte/issues/5085), [Docs](https://v4.svelte.dev/docs#template-syntax-element-directives-on-eventname))
  - Add `axis` parameter to `slide` transition ([#6182](https://github.com/sveltejs/svelte/issues/6182), [Docs](https://v4.svelte.dev/docs#run-time-svelte-transition-slide))
  - Add `readonly` utility to convert `writable` store to readonly ([#6518](https://github.com/sveltejs/svelte/pull/6518), [Docs](https://v4.svelte.dev/docs#run-time-svelte-store-writable))
  - Add `readyState` binding for media elements ([#6666](https://github.com/sveltejs/svelte/issues/6666), [Docs](https://v4.svelte.dev/docs#template-syntax-element-directives-bind-property-media-element-bindings))
  - Add `naturalWidth` and `naturalHeight` bindings to images ([#7771](https://github.com/sveltejs/svelte/issues/7771), [Docs](https://v4.svelte.dev/docs#template-syntax-element-directives-bind-property-image-element-bindings))
- Support `<!-- svelte-ignore ... -->` on components ([#8082](https://github.com/sveltejs/svelte/issues/8082))
- Inputs in a `bind:group` will clear when their value is set to `undefined` (**3.56.0**, [#8214](https://github.com/sveltejs/svelte/issues/8214))
- `<input>` values will now persist when swapping elements with spread attributes in an `{#each}` block (**3.56.0**, [#7578](https://github.com/sveltejs/svelte/issues/7578))
- Better warnings across the board - from `noreferrer` to `aria` rules (**3.56.0**)
- Add <svelte:document> (**3.57.0**, [#3310](https://github.com/sveltejs/svelte/issues/3310))
- The `style:` directive will now take precedence over a `style=` attribute (**3.57.0**, [#7475](https://github.com/sveltejs/svelte/issues/7475))
- CSS units are now supported in the `fly` and `blur` transitions (**3.57.0**, [#7623](https://github.com/sveltejs/svelte/pull/7623), [Docs](https://v4.svelte.dev/docs#run-time-svelte-transition))

Svelte コンパイラに対する全ての変更については、まだ未リリースの変更も含め、[CHANGELOG](https://github.com/sveltejs/svelte/blob/master/CHANGELOG.md)  をご確認ください。

## What's new in SvelteKit

- You can now get all cookies for a request with `cookies.getAll` (**1.10.0**, [#9287](https://github.com/sveltejs/kit/pull/9287), [Docs](/docs/kit/@sveltejs-kit#Cookies))
- Easily manage the submission status of (multiple) forms with the new exposed `submitter` parameter in `use:enhance` (**1.12.0**, [#9425](https://github.com/sveltejs/kit/pull/9425), [Docs](/docs/kit/@sveltejs-kit#SubmitFunction))
- The default error page now has dark mode styles (**1.13.0**, [#9460](https://github.com/sveltejs/kit/pull/9460))
- You can now omit types on all methods and variables with special meaning to SvelteKit and still benefit from full type safety! Read more about it in the [announcement blog post](/blog/zero-config-type-safety)

---

## Community Showcase

### Apps & Sites built with Svelte

- [Peerbeer](https://peer.beer/) lets you share files peer-to-peer (p2p) without any third parties or data limits
- [unplaneted](https://unplaneted.com/) is an interface for exploring very large space images
- [PokeBook](https://github.com/pokegh0st/pokebook) is a digital notebook for writing poetry that provides a beautiful distraction-free environment and autosave
- [papi](https://papi.run/) lets you create prompts for AI models and share them with others with a unique link
- [Mathesar](https://github.com/centerofci/mathesar) is a straightforward open source tool that provides a spreadsheet-like interface to a PostgreSQL database
- [SQLite Playground](https://neil.macmunn.com/sqlite#) lets you learn how SQLite runs and stores data in the browser
- [svgl](https://github.com/pheralb/svgl) is a beautiful library with SVG logos
- [Swehl](https://swehl.com/) is an eCommerce store, community and tutorial site for breastfeeding mothers
- [Codeverter](https://github.com/TGlide/codeverter) is a GPT-powered code converter, allowing you to convert between different languages and frameworks
- [Game On Or Not](https://gameonornot.com/) is a free web app that helps you organize sports with your friends
- [Sveltia CMS](https://github.com/sveltia/sveltia-cms) is a Git-based lightweight headless CMS

### Learning Resources

_Featuring Svelte Contributors and Ambassadors_

- [Streaming, snapshots, and other new features since SvelteKit 1.0](/blog/streaming-snapshots-sveltekit) by Geoff Rich on the svelte.dev Blog
- [Dev Vlog: Rich Harris shows us what's new in Svelte and Kit, March 2023](https://www.youtube.com/watch?v=vgXgex5E-8g) from Svelte Society
  - If you missed this one live, check out [the next one](https://www.youtube.com/watch?v=MJHO6FSioPI) - scheduled for April 5th
- [Svelte Society - London February 2023](https://www.youtube.com/watch?v=RkQ_f7XxdMI)
- Svelte Radio episodes from this month:
  - [We all live in a Svelte Submarine](https://www.svelteradio.com/episodes/we-all-live-in-a-svelte-submarine)
  - [Building furniture using Svelte with Bert Bengtson](https://www.svelteradio.com/episodes/building-furniture-using-svelte-with-bert-bengtson)
  - [Svelte Hackathon Announcement](https://www.svelteradio.com/episodes/svelte-hackathon-announcement)
  - [LevelUpTuts 6 months later with Scott Tolinski](https://www.svelteradio.com/episodes/leveluptuts-6-months-later-with-scott-tolinski)
  - [I got a cold and had fever dreams about React 😱](https://www.svelteradio.com/episodes/i-got-a-cold-and-had-fever-dreams-about-react)
- This Week In Svelte videos:
  - [2023 March 10 - New prompts! Underline your links!](https://www.youtube.com/watch?v=WiCjQVoE-3k)
  - [2023 March 17 - More a11y warnings! How to: Dynamic Form Actions!](https://www.youtube.com/watch?v=sRhZQ-2VxVU)
  - [2023 March 23 - SvelteKit 1.13.0, Vitest and Playwright overview](https://www.youtube.com/watch?v=vpbhsbg2otg)

_To Watch or Hear_

- [Full Stack SvelteKit App Deployment Using Vercel And Supabase For $0](https://www.youtube.com/watch?v=uAF4Yd-gddo) by Joy of Code
- [Why Is Svelte.js so Popular?](https://www.youtube.com/watch?v=73Y8Yyg54zc) by Prismic
- [Interactive Tables in SvelteKit with TanStack Table](https://www.youtube.com/watch?v=-Zuo3UWjjI8) by hartenfellerdev
- [SvelteKit + GraphQL with Houdini](https://www.youtube.com/watch?v=ADnaRwQZfqw&list=PLm0ILX0LGQk_220vvpsbyXH2VesRlCm-E) by Aftab Alam

_To Read_

- [Thoughts on Svelte](https://tyhopp.com/notes/thoughts-on-svelte) by Ty Hopp
- [Storybook](https://storybook.js.org/blog/storybook-for-sveltekit/) on why (and how) it supports SvelteKit
- [Svelte Authentication Tutorial with Authorizer](https://thethinks.vercel.app/blog/svelte-authorizer) by The Thinks
- [Use Zod to Validate Forms on the Server with SvelteKit](https://blog.robino.dev/posts/svelte-zod-error) by Ross Robino
- [Do I need a sitemap for my SvelteKit app, and how do I create it?](https://maier.tech/posts/do-i-need-a-sitemap-for-my-sveltekit-app-and-how-do-i-create-it) and [Complement zero-effort type safety in SvelteKit with Zod for even more type safety](https://maier.tech/posts/complement-zero-effort-type-safety-in-sveltekit-with-zod-for-even-more-type-safety) and [Configuring Turborepo for a SvelteKit monorepo](https://maier.tech/posts/configuring-turborepo-for-a-sveltekit-monorepo) by Thilo Maier
- [Adding page transitions in SvelteKit](https://joshcollinsworth.com/blog/sveltekit-page-transitions) by Josh Collinsworth
- [E2E testing with SvelteKit and Playwright](https://www.okupter.com/blog/e2e-testing-with-sveltekit-and-playwright) and [Why you should use TypeScript in your next SvelteKit projects](https://www.okupter.com/blog/sveltekit-with-typescript) by Justin Ahinon
- [Understanding the structure of a SvelteKit project](https://www.inow.dev/understanding-the-structure-of-a-svelte-kit-project/) by Igor Nowosad
- [Secure Authentication in Svelte using Hooks](https://dev.to/brewhousedigital/secure-authentication-in-svelte-using-hooks-k5j) by Brewhouse Digital

### Libraries, Tools & Components

- [@vavite/node-loader](https://github.com/cyco130/vavite/tree/main/packages/node-loader) is a Node ESM loader that uses Vite to transpile modules to enable sourcemap and breakpoints support in SvelteKit (or any Vite) project
- [Inlang](https://github.com/inlang/inlang) is building i18n for SvelteKit and is [looking for feedback](https://www.reddit.com/r/sveltejs/comments/11ydtui/sveltekit_and_i18n_lets_finally_solve_this_never/)
- [Skeleton](https://www.skeleton.dev/) - the UI toolkit for Svelte and Tailwind - is now 1.0 🎉
- [SvelteKit-integrated-WebSocket](https://github.com/suhaildawood/SvelteKit-integrated-WebSocket) provides first-class support for WebSockets within SvelteKit by attaching a WebSocket server to the global state
- [Svelte Legos](https://github.com/ankurrsinghal/svelte-legos) is a collection of essential Svelte Composition Utilities
- [svelte-stored-writable](https://github.com/efstajas/svelte-stored-writable) is a drop-in extension of Svelte's writable that additionally stores and restores its contents using localStorage.
- [svelte-virtual](https://github.com/ghostebony/svelte-virtual) provides Svelte components for efficiently rendering large lists.
- ChatGPT Clones and Starters
  - [chatwithme.chat](https://github.com/kierangilliam/chatwithme.chat) is an open source ChatGPT UI
  - [SlickGPT](https://github.com/ShipBit/slickgpt) is a light-weight "use-your-own-API-key" web client for the OpenAI API written in Svelte
  - [AI Chat Bestie](https://github.com/KTruong008/aichatbestie) is an unofficial ChatGPT app
  - [chatgpt-svelte](https://github.com/ichbtrv/chatgpt-svelte) is a simple UI for the ChatGPT Open AI API

お読みいただきありがとうございました！あと、[Svelte Hackathon](https://hack.sveltesociety.dev/) にも是非チャレンジしてみてください 🧑‍💻

いつも通り、見落としなどございましたら [Reddit](https://www.reddit.com/r/sveltejs/) や [Discord](https://discord.gg/svelte) にてお気軽にお知らせください。

また次回お会いしましょう！
