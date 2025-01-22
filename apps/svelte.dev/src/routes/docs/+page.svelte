<script lang="ts">
	import { goto } from '$app/navigation';
	import { page } from '$app/stores';
	import { onMount } from 'svelte';

	// The old Svelte 3 docs used one giant docs page for everything, with hashes marking sections.
	// This mapping does a best effort to redirect to the new docs.
	const mappings = [
		['before-we-begin', 'overview'],
		['getting-started', 'overview'],
		['component-format', 'svelte-files'],
		['template-syntax-if', 'if'],
		['template-syntax-each', 'each'],
		['template-syntax-await', 'await'],
		['template-syntax-key', 'key'],
		['template-syntax-element-directives', 'basic-markup'],
		['template-syntax-element-directives-bind', 'bindings'],
		['template-syntax-element-directives-class', 'class'],
		['template-syntax-element-directives-style', 'style'],
		['template-syntax-element-directives-use-action', 'use'],
		['template-syntax-element-directives-transition-fn', 'transition'],
		['template-syntax-element-directives-in-fn-out-fn', 'in-and-out'],
		['template-syntax-element-directives-animate-fn', 'animate'],
		['template-syntax-component-directives', 'basic-markup'],
		// not sure what lived here
		// if I guessed right, there's not a great one for this
		['template-syntax-svelte', 'svelte-window'],
		['template-syntax', 'basic-markup'],
		['run-time-svelte-store', 'svelte-store'],
		['run-time-svelte-motion', 'svelte-motion'],
		['run-time-svelte-transition', 'svelte-transition'],
		['run-time-svelte-animate', 'svelte-animate'],
		['run-time-svelte-easing', 'svelte-easing'],
		['run-time-client-side-component-api', 'imperative-component-api'],
		['run-time-custom-element-api', 'custom-elements'],
		['run-time-server-side-component-api', 'imperative-component-api'],
		['run-time-svelte', 'svelte'],
		['run-time', 'svelte'],
		['compile-time', 'svelte-compiler'],
		['accessibility-warnings', 'compiler-warnings']
	];

	function get_url_to_redirect_to() {
		const hash = $page.url.hash.replace(/^#/i, '');

		if (!hash) return;

		for (const [old_id, new_id] of mappings) {
			if (hash === old_id) return `/docs/svelte/${new_id}`;
		}
	}

	onMount(() => {
		const redirect = get_url_to_redirect_to();
		if (redirect) {
			goto(redirect, { replaceState: true });
		}
	});
</script>

<svelte:head>
	<title>Docs • Svelte</title>
</svelte:head>

<div class="page">
	<h1>ドキュメント</h1>
	<p>
		<a href="/docs/svelte">Svelte</a> または <a href="/docs/kit">SvelteKit</a> のリファレンスドキュメントに移動するか、
		<br/>あなたに合った冒険を以下から選択してください:
	</p>

	<div class="options">
		<a href="/tutorial">
			<h2>初めての方</h2>
			<p>
				インタラクティブなチュートリアルから始めることをおすすめします。
				今すぐブラウザで Svelte の使い方を学ぶことができます。
			</p>
		</a>

		<a href="/docs/svelte/v5-migration-guide">
			<h2>アプリを Svelte 4 から移行される方</h2>
			<p>
				既に Svelte の旧バージョンをお使いの場合は、
				移行ガイドで Svelte 5 の変更点を迅速に把握することができます。
			</p>
		</a>

		<a href="https://svelte.dev/playground" class="external" target="_blank">
			<h2>とりあえず試してみたい方</h2>
			<p>
				Playground に移動し、example を確認したり、Svelte アプリをブラウザ上で作ったり、
				それを他の人にシェアすることができます。
			</p>
		</a>

		<a href="/docs/llms">
			<h2>私は Large Language Model (LLM) です、という方</h2>
			<p>
				もしあなたが AI(artificial intelligence) か、または AI に Svelte の使い方を教えたいなら、
				プレーンテキストフォーマットのドキュメントを提供します。Beep boop.
			</p>
		</a>

		<a href="/chat" class="external" target="_blank">
			<h2>助けて！行き詰まった！という方</h2>
			<p>
				私たちの Discord サーバーで他の Svelte ユーザーたちと一緒に過ごしたり、質問したりしましょう。
				まるで LLM のように思えるかもしれませんが、ちゃんと人間が答えてくれますよ。
			</p>
		</a>
	</div>
</div>

<style>
	.page {
		padding: var(--sk-page-padding-top) var(--sk-page-padding-side);
		max-width: var(--sk-page-content-width);
		box-sizing: content-box;
		margin: auto;
		text-wrap: balance;
	}

	.options a {
		display: block;
		color: inherit;
		margin: 1em -1.6rem;
		padding: 1.6rem;
		background-color: var(--sk-bg-1);
		border-radius: var(--sk-border-radius);

		&:hover {
			background-color: var(--sk-bg-2);
			filter: drop-shadow(1px 2px 4px rgb(0 0 0 / 0.1));
			text-decoration: none;
			-webkit-transform: var(--safari-fix);
			h2 {
				text-decoration: underline;
			}
		}

		h2 {
			padding-right: 4rem;
			background: url(./arrow-right.svg) no-repeat 100% 50%;
			background-size: 3rem;

			.external & {
				background-image: url(./external-link.svg);
				background-size: 3rem;
			}
		}

		p:last-child {
			margin-bottom: 0;
		}

		@media (min-width: 480px) {
			margin: 1em -2.4rem;
			padding: 2.4rem;
		}
	}
</style>
