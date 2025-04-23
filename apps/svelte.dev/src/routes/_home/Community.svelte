<script>
	import { Section } from '@sveltejs/site-kit/components';
</script>

<Section --max-width="200rem">
	<h2>私たちのフレンドリーなコミュニティに参加しませんか</h2>
	<p>
		私たちの姉妹組織である <a href="https://www.sveltesociety.dev/">Svelte Society</a> は、世界中でイベントを運営しています。
	    あなたが所属する支部を見つけに、
		<a href="/chat">Discord サーバー</a>に参加しましょう。
	</p>

	<figure>
		<enhanced:img
			class="collage"
			src="./summit.png?w=800;1200;2000;2800;4400"
			alt="Photos by Marcel Cutts from the 2022 Svelte Summit in Stockholm"
		/>
		<figcaption>Photos by <a href="https://marcel.gg/">Marcel Cutts</a></figcaption>
	</figure>
</Section>

<style>
	figure {
		position: relative;
	}

	figcaption {
		position: relative;
		top: max(-2vw, calc(-0.02 * (120rem + 2 * var(--sk-page-padding-side))));
		font: var(--sk-font-ui-medium);
		margin: 0 auto;
		padding: 0 var(--sk-page-padding-side);
		color: var(--sk-fg-3);
		text-align: center;

		a {
			text-wrap: nowrap;
			color: inherit;
			text-decoration: underline;
		}
	}

	.collage {
		width: 100%;
		height: auto;
	}

	h2,
	p {
		text-align: center;
	}

	p {
		max-width: 28em;
		margin-left: auto;
		margin-right: auto;
	}
</style>
