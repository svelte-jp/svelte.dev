---
title: Sharing code
---

これまで見てきたすべての例では、`<script>` ブロックには各コンポーネントのインスタンスが初期化されたときに実行されるコードが含まれています。大部分のコンポーネントでは、これだけで十分です。

ごく稀に、個々のコンポーネントのインスタンスの外でコードを実行しなければならないことがあります。例えば、[以前の演習](media-elements) のカスタムオーディオプレーヤーを振り返ると、4つの曲を同時に再生することができましたが、1つを再生すると他のすべてのオーディオプレーヤーが停止した方がより良いでしょう。

これを実現するには、`<script module>` ブロックを宣言します。ここに含まれるコードは、コンポーネントがインスタンス化されたときではなく、モジュールが最初に評価されたときに一度だけ実行されます。これを `AudioPlayer.svelte` の先頭に配置してください (これは _別個の_ script タグであることにご注意ください)。

```svelte
/// file: AudioPlayer.svelte
+++<script module>
	let current;
</script>+++
```

これで状態を管理することなく、コンポーネント同士がお互いに「会話」することが可能になりました。

```svelte
/// file: AudioPlayer.svelte
<audio
	src={src}
	bind:currentTime={time}
	bind:duration
	bind:paused
+++	onplay={(e) => {
		const audio = e.currentTarget;

		if (audio !== current) {
			current?.pause();
			current = audio;
		}
	}}+++
	onended={() => {
		time = 0;
	}}
/>
```
