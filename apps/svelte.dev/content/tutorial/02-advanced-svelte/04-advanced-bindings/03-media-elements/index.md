---
title: Media elements
---

`<audio>` 要素と `<video>` 要素のプロパティをバインドすることができるので、(例えば) `AudioPlayer.svelte` のようなカスタムのプレーヤー UI をとても簡単に作ることができます。

最初に、`<audio>` 要素とそのバインディングを追加します (`src` と `duration` と `paused` は短縮形を使います):

```svelte
/// file: AudioPlayer.svelte
<div class="player" class:paused>
+++	<audio
		{src}
		bind:currentTime={time}
		bind:duration
		bind:paused
	></audio>+++

	<button
		class="play"
		aria-label={paused ? 'play' : 'pause'}
	></button>
```

次に、`paused` を切り替える `<button>` にイベントハンドラを追加します:

```svelte
/// file: AudioPlayer.svelte
<button
	class="play"
	aria-label={paused ? 'play' : 'pause'}
	+++onclick={() => paused = !paused}+++
></button>
```

これでオーディオプレーヤーに基本的な機能が付きました。では、スライダーをドラッグして曲の指定した部分にシークできる機能を追加しましょう。スライダー(slider)の `pointerdown` ハンドラの内側にある `seek` 関数で、`time` を更新することができます:

```js
/// file: AudioPlayer.svelte
function seek(e) {
	const { left, width } = div.getBoundingClientRect();

	let p = (e.clientX - left) / width;
	if (p < 0) p = 0;
	if (p > 1) p = 1;

	+++time = p * duration;+++
}
```

曲が終わったら、親切に巻き戻しましょう:

```svelte
/// file: AudioPlayer.svelte
<audio
	{src}
	bind:currentTime={time}
	bind:duration
	bind:paused
+++	onended={() => {
		time = 0;
	}}+++
></audio>
```

`<audio>` と `<video>` のバインディングの完全なセットは以下の通りです — 7つの _読み取り専用(readonly)_ のバインディング…

- `duration` — 総再生時間 (秒単位)
- `buffered` — `{start, end}` オブジェクトの配列
- `seekable` — 同上
- `played` — 同上
- `seeking` — boolean
- `ended` — boolean
- `readyState` — 0 から 4 までの数値 (0 と 4 も含む)

…と5つの _双方向_ バインディングです:

- `currentTime` — 再生マーカー (playhead) の現在の位置 (秒単位)
- `playbackRate` — 再生速度を上げるか遅くするか (`1` が 'normal')
- `paused` — これは自明ですね
- `volume` — 0 から 1 の値
- `muted` — boolean で、true はミュートを意味します

video には読み取り専用の `videoWidth` と `videoHeight` バインディングがあります。
