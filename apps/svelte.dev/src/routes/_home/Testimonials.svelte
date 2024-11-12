<div class="outer">
	<p class="definition">
		<enhanced:img
			class="pronunciation"
			alt="Svelte pronunciation guide"
			src="./svelte-pronunciation.svg"
		/>

		<span class="description">
			<span class="adjective"></span> 魅力的でスリム、優雅でスタイリッシュ
		</span>
	</p>

	<div class="blurb">
		<p>
			Svelte はコンパイラを使用する UI フレームワークで、息を呑むほど簡潔にコンポーネントを記述でき、
			ブラウザで最小限の動作となるようにしてくれます。開発者には既知の言語である HTML、CSS、JavaScript を使うことができます。
			<strong>これは、web 開発へのラブレターです。</strong>
		</p>

		<p>
			私たちだけでなく、常に開発者たちからも、Svelte は使用する上で最もエキサイティングなフレームワークとしてランク付けされています。
		</p>
	</div>

	<!-- svelte-ignore a11y_consider_explicit_label (the <enhanced:img> alt takes care of it)-->
	<div class="screenshots">
		<a href="https://survey.stackoverflow.co/2024/technology#2-web-frameworks-and-technologies">
			<enhanced:img
				class="screenshot"
				alt="Stack Overflow 2024 Developer Survey"
				src="./stack-overflow.png?w=1200,1600"
			></enhanced:img>
		</a>

		<a href="https://2023.stateofjs.com/en-US/libraries/front-end-frameworks/">
			<enhanced:img
				class="screenshot"
				alt="State of JavaScript 2023"
				src="./state-of-js-chart.png?w=1000,1400"
			></enhanced:img>
		</a>

		<a href="https://x.com/flaviocopes/status/1730895911864189299">
			<enhanced:img class="screenshot" alt="Tweet from @flaviocopes" src="./flavio-light.png?w=800"
			></enhanced:img>
		</a>
	</div>
</div>

<style>
	.outer {
		position: relative;
		max-width: 120rem;
		margin: 4rem auto;
		padding: 0 var(--sk-page-padding-side);
		display: grid;
		row-gap: 4rem;
		grid-template-areas:
			'definition'
			'blurb'
			'screenshots';
	}

	.definition {
		grid-area: definition;
	}

	.pronunciation {
		position: relative;
		aspect-ratio: 457.4 / 138.8;
		height: var(--sk-font-size-h1);
		bottom: -0.3em;
	}

	.blurb {
		grid-area: blurb;
	}

	.screenshots {
		grid-area: screenshots;
		position: relative;
		width: 100%;
		aspect-ratio: 16 / 10;

		a {
			position: absolute;
			display: block;
			width: 100%;
			top: 0;
			overflow: hidden;
			filter: drop-shadow(0.2rem 0.4rem 1.6rem rgb(0 0 0 / 0.2));
			transform: translate3d(0, 0, 0);
			transition-property: filter, scale;
			transition-duration: 0.2s;
			user-select: none;
			will-change: filter, transform;

			&:nth-child(1) {
				top: 0%;
				left: -2%;
				rotate: -1deg;
			}

			&:nth-child(2) {
				width: 80%;
				left: 22%;
				top: 32%;
				rotate: -0.7deg;
			}

			&:nth-child(3) {
				top: 51%;
				left: 5%;
				width: 50%;
				rotate: 1.5deg;
			}

			@media all and not (hover: none) {
				&:hover {
					scale: 1.05;
					filter: drop-shadow(0.2rem 0.4rem 2.4rem rgb(0 0 0 / 0.2));
				}
			}
		}

		.screenshot {
			width: 100%;
			height: auto;
			object-fit: contain;
			border-radius: var(--sk-border-radius);
			transition: filter 0.2s;
			-webkit-transform: var(--safari-fix);

			@media all and not (hover: none) {
				/* the additional `contrast(1)` is necessary for safari 18 to not behave stupidly */
				filter: grayscale(1) contrast(1);

				a:hover & {
					filter: grayscale(0) contrast(1);
				}
			}
		}
	}

	.definition {
		position: relative;
		display: flex;
		align-items: start;
		justify-content: center;
		margin: 0 auto;
		gap: 1rem;

		width: 100%;

		.description {
			position: relative;
			font: var(--sk-font-ui-medium);
			font-feature-settings: "palt";
			bottom: 0.2em;
			text-wrap: balance;
			width: 16rem;
		}

		.adjective {
			position: relative;
			padding: 0.25em 0.5em;
			line-height: 1;
			text-transform: uppercase;
			background: var(--sk-fg-2);
			border-radius: var(--sk-border-radius);
			font: var(--sk-font-ui-small);
			color: var(--sk-bg-2);

			&::after {
				content: 'adj.';
			}
		}
	}

	@media (min-width: 800px) {
		.definition {
			align-items: baseline;
			justify-content: start;

			.description {
				flex-direction: row;
				gap: 1rem;
				width: auto;
			}

			.adjective {
				margin-right: 0.5rem;

				&::after {
					content: '形容詞';
				}
			}
		}
	}

	@media (min-width: 960px) {
		.outer {
			display: grid;
			margin: 4em auto;
			grid-template-columns: minmax(0, 1fr) minmax(0, 1fr);
			column-gap: 4rem;
			grid-template-areas:
				'definition definition'
				'blurb      screenshots';

			.blurb {
				text-wrap: balance;
			}
		}
	}

	@media (min-width: 1140px) {
		.screenshots {
			top: -7em;
		}
	}
</style>
