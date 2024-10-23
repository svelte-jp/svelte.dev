---
title: 概要
---

Svelte は Web 上のユーザーインターフェースを構築するためのフレームワークです。Svelte はコンパイラを使用し、HTML、CSS、JavaScript で記述された宣言的なコンポーネントを...

```svelte
<!--- file: App.svelte --->
<script>
	function greet() {
		alert('Welcome to Svelte!');
	}
</script>

<button onclick={greet}>click me</button>

<style>
	button {
		font-size: 2em;
	}
</style>
```

...無駄のない、タイトで最適化された JavaScript に変換します。

これにより、スタンドアローンなコンポーネントからフルスタックアプリ (Svelte のアプリケーションフレームワークである [SvelteKit](../kit) を使用) まで、お望みのものをなんでも構築することができます。

こちらのページはリファレンスドキュメントとして提供されています。もしあなたが Svelte の初心者なら、先に[インタラクティブなチュートリアル](/tutorial)から始めて、わからないことがあるときにこちらに戻ってくることをおすすめします。

また、[Playground](/playground) を使ってオンラインで Svelte を試すこともできますし、より高機能な環境が必要なら [StackBlitz](https://sveltekit.new) で試すこともできます。
