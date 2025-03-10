---
title: Springs
---

`Spring` クラスは `Tween` の代替であり、頻繁に変更される値に対してより適切に機能することがよくあります。

この例では、マウスに追従する円と、円の座標とサイズの 2 つの値があります。これらをスプリングに変換してみましょう。

```svelte
/// file: App.svelte
<script>
	+++import { Spring } from 'svelte/motion+++';

	let coords = +++new Spring+++({ x: 50, y: 50 });
	let size = +++new Spring+++(10);
</script>
```

`Tween` と同様に、スプリングには書き込み可能な `target` プロパティと読み取り専用の `current` プロパティがあります。イベントハンドラーを更新します...

```svelte
<svg
	onmousemove={(e) => {
		coords.+++target+++ = { x: e.clientX, y: e.clientY };
	}}
	onmousedown={() => (size.+++target+++ = 30)}
	onmouseup={() => (size.+++target+++ = 10)}
	role="presentation"
>
```

...そして `<circle>` 属性も更新します。

```svelte
<circle
	cx={coords.+++current+++.x}
	cy={coords.+++current+++.y}
	r={size.+++current+++}
></circle>
```

どちらのスプリングにもデフォルトの `stiffness` と `damping` の値があり、スプリングの弾力性を制御します。独自の初期値を指定できます。

```js
/// file: App.svelte
let coords = new Spring({ x: 50, y: 50 }, +++{
	stiffness: 0.1,
	damping: 0.25
}+++);
```

マウスを動かしてスライダーをドラッグし、スプリングの動作にどのような影響を与えるかを確認してください。スプリングが動いている間に値を調整できることに注意してください。
