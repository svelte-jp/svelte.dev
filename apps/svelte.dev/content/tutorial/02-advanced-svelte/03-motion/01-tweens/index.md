---
title: Tweened values
---

大抵の場合、値が変化していることを伝えるには、 _motion_ を使用するのが良い方法です。Svelteでは、ユーザーインターフェースに motion を追加するためのクラスを提供しています。

`Tween` クラスを `svelte/motion` からインポートしましょう:

```svelte
/// file: App.svelte
<script>
	+++import { Tween } from 'svelte/motion';+++

	let progress = $state(0);
</script>
```

`progress` に `Tween` のインスタンスを代入します:

```svelte
/// file: App.svelte
<script>
	import { Tween } from 'svelte/motion';

	let progress = +++new Tween+++(0);
</script>
```

`Tween` クラスには書き込み可能な `target` プロパティと、読み取り専用の `current` プロパティを持っています — `<progress>` 要素を更新します...

```svelte
<progress value={progress.+++current+++}></progress>
```

...そして各イベントハンドラーも更新します:

```svelte
<button onclick={() => (progress.+++target+++ = 0)}>
	0%
</button>
```

ボタンをクリックするとプログレスバーが新たな値に合わせてアニメーションします。まだ少しロボット的でまだ満足いくようなものではありませんね。easing 関数を追加する必要があります:

```svelte
/// file: App.svelte
<script>
	import { Tween } from 'svelte/motion';
	+++import { cubicOut } from 'svelte/easing';+++

	let progress = new Tween(0, +++{
		duration: 400,
		easing: cubicOut
	}+++);
</script>
```

> [!NOTE] `svelte/easing` モジュールには [Penner easing equations](https://web.archive.org/web/20190805215728/http://robertpenner.com/easing/) が含まれていますが、`p` と `t` の両方が 0 から 1 の間の値を取る独自の `p => t` 関数を指定することもできます。

`Tween` で利用可能なオプションの一覧です。

- `delay` — tween 開始までのミリ秒
- `duration` — ミリ秒単位の tween の持続時間、または(例えば値の変化が大きい場合に、より長い tween を指定出来るようにするための）`(from, to) => milliseconds` 関数
- `easing` — `p => t` 関数
- `interpolate` — 任意の値の間を補間するための自前の `(from, to) => t => value` 関数。デフォルトでは、Svelte は数値や日付、同じ形の配列やオブジェクトの間を補間します (数値や日付、その他の有効な配列やオブジェクトのみを含む場合に限ります)。(例えば) 色文字列や変換行列を補間したい場合は、自前の関数を指定してください。

`progress.target` に直接代入する代わりに、`progress.set(value, options)` を呼び出すこともできます。この場合、`options` はデフォルトをオーバーライドします。`set` メソッドは tween が完了した時点で resolve される promise を返します。
