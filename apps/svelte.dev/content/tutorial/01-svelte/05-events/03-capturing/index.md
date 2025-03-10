---
title: Capturing
---

通常、イベントハンドラーは [_バブリング_](https://developer.mozilla.org/ja/docs/Learn/JavaScript/Building_blocks/Event_bubbling) フェーズで実行されます。この例で `<input>` に何かを入力すると何が起こるかに注目してください。イベントが _target_ から _document_ まで「バブル」すると、最初に内部ハンドラーが実行され、その後に外部ハンドラーが実行されます。

場合によっては、代わりに _capture_ フェーズ中にハンドラを実行したいことがあります。イベント名の末尾に `capture` を追加します。

```svelte
/// file: App.svelte
<div onkeydown+++capture+++={(e) => alert(`<div> ${e.key}`)} role="presentation">
	<input onkeydown+++capture+++={(e) => alert(`<input> ${e.key}`)} />
</div>
```

現在、相対的な順序は逆になっています。特定のイベントに対してキャプチャハンドラーと非キャプチャハンドラーの両方が存在する場合、キャプチャハンドラーが最初に実行されます。
