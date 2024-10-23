---
title: イントロダクション
---

## Before we begin

> [!NOTE] Svelte や SvelteKit が初めてなら、こちらの[インタラクティブなチュートリアル](/tutorial)をチェックしてみることをおすすめします。
>
> 行き詰まったら、[Discord chatroom](https://svelte.dev/chat) でヘルプを求めてください。

## What is SvelteKit?

SvelteKit は、[Svelte](https://svelte.dev/) を使用して堅牢でハイパフォーマンスな web アプリケーションを迅速に開発するためのフレームワークです。もしあなたが React 界隈から来たのであれば、SvelteKit は Next に似ているものです。Vue 界隈から来たのであれば、Nuxt に似ています。

SvelteKit で構築することのできるアプリケーションの種類については、[FAQ](faq#What-can-I-make-with-SvelteKit) をご覧ください。

## What is Svelte?

In short, Svelte is a way of writing user interface components — like a navigation bar, comment section, or contact form — that users see and interact with in their browsers. The Svelte compiler converts your components to JavaScript that can be run to render the HTML for the page and to CSS that styles the page. You don't need to know Svelte to understand the rest of this guide, but it will help. If you'd like to learn more, check out [the Svelte tutorial](https://svelte.dev/tutorial).

## SvelteKit vs Svelte

Svelte renders UI components. You can compose these components and render an entire page with just Svelte, but you need more than just Svelte to write an entire app.

SvelteKit helps you build web apps while following modern best practices and providing solutions to common development challenges. It offers everything from basic functionalities — like a [router](glossary#Routing) that updates your UI when a link is clicked — to more advanced capabilities. Its extensive list of features includes [build optimizations](https://vitejs.dev/guide/features.html#build-optimizations) to load only the minimal required code; [offline support](service-workers); [preloading](link-options#data-sveltekit-preload-data) pages before user navigation; [configurable rendering](page-options) to handle different parts of your app on the server via [SSR](glossary#SSR), in the browser through [client-side rendering](glossary#CSR), or at build-time with [prerendering](glossary#Prerendering); [image optimization](images); and much more. Building an app with all the modern best practices is fiendishly complicated, but SvelteKit does all the boring stuff for you so that you can get on with the creative part.

It reflects changes to your code in the browser instantly to provide a lightning-fast and feature-rich development experience by leveraging [Vite](https://vitejs.dev/) with a [Svelte plugin](https://github.com/sveltejs/vite-plugin-svelte) to do [Hot Module Replacement (HMR)](https://github.com/sveltejs/vite-plugin-svelte/blob/main/docs/config.md#hot).
