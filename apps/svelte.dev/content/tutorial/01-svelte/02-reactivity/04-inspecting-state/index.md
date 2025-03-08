---
title: Inspecting state
---

時間の経過とともに変化する状態の値を追跡できることは、多くの場合便利です。

今回は`addNumber` 関数内に `console.log` ステートメントを追加しました。ただし、ボタンをクリックした後にDevコンソールを開くと、警告と、メッセージを複製できなかったというメッセージが表示されます。

これは、`numbers` がリアクティブ [プロキシ](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Proxy) であるためです。できることはいくつかあります。まず、`$state.snapshot(...)` を使用して、状態の非リアクティブ _スナップショット_ を作成できます。

```js
/// file: App.svelte
function addNumber() {
	numbers.push(numbers.length + 1);
	console.log(+++$state.snapshot(numbers)+++);
}
```

あるいは、`$inspect` ルーンを使用して、状態が変化するたびにそのスナップショットを自動的に記録することもできます。このコードは、プロダクションビルドから自動的に削除されます。

```js
/// file: App.svelte
function addNumber() {
	numbers.push(numbers.length + 1);
	---console.log($state.snapshot(numbers));---
}

+++$inspect(numbers);+++
```

`$inspect(...).with(fn)` を使用すると、情報の表示方法をカスタマイズできます。たとえば、`console.trace` を使用して、状態の変化の発生元を確認できます。

```js
/// file: App.svelte
$inspect(numbers)+++.with(console.trace)+++;
```
