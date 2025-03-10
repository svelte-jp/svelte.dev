---
title: Effects
---

これまで、状態の観点から反応性について説明してきました。しかし、それは物事のまだ半分( _half of the equation_ )に過ぎません。状態は、何かがそれに _反応している場合_ にのみ反応性があり、そうでない場合は単なる特殊な変数( _sparkling variable_ )です。

反応するものは _effect_ と呼ばれます。すでにエフェクト (状態の変化に応じて DOM を更新するために Svelte が作成するエフェクト) について説明しましたが、`$effect` ルーンを使用して独自のエフェクトを作成することもできます。

> [!NOTE] ほとんどの場合、`$effect` を使用するべきではありません。`$effect` は頻繁に使用するものではなく、困った時の最終手段として考えるのが最適です。たとえば、副作用( _side effects_ )を [イベント ハンドラー](dom-events) に配置できるのであれば、ほとんどの場合それが望ましいです。

`setInterval` を使用して、コンポーネントがマウントされている時間を追跡するとします。エフェクトを作成します。

```svelte
/// file: App.svelte
<script>
	let elapsed = $state(0);
	let interval = $state(1000);

+++	$effect(() => {
		setInterval(() => {
			elapsed += 1;
		}, interval);
	});+++
</script>
```

speed upボタンを数回クリックすると、`interval` が小さくなるたびに `setInterval` が呼び出されるため、`elapsed` がより速く増加することがわかります。

次にslow downボタンをクリックしても、うまくいきません。これは、エフェクトの更新時に古い間隔をクリアしていないためです。クリーンアップ関数を返すことでこれを修正できます。

```js
/// file: App.svelte
$effect(() => {
	+++const id =+++ setInterval(() => {
		elapsed += 1;
	}, interval);

+++	return () => {
		clearInterval(id);
	};+++
});
```

クリーンアップ関数は、`interval` が変更されたとき、およびコンポーネントが破棄されたときに、エフェクト関数が再実行される直前に呼び出されます。

エフェクト関数が実行時に状態を読み取らない場合は、コンポーネントがマウントされるときに 1 回だけ実行されます。

> [!NOTE] サーバー側のレンダリング中は`$effect`は実行されません。
