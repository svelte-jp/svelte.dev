---
title: Param matchers
path: /colors/ff3e00
---

ルーターが無効な入力にマッチするのを防ぐために、 _matcher_ を指定することができます。例えば、`/colors/[value]` のようなルート(route)を、`/colors/ff3e00` のような16進数の値(hex value)にマッチさせたいけれど、`/colors/octarine` のような色の名前やその他の任意の入力にはマッチさせたくないことがあるでしょう。

まず、`src/params/hex.js` という新しいファイルを作成し、そこから `match` 関数をエクスポートしてください。

```js
/// file: src/params/hex.js
export function match(value) {
	return /^[0-9a-f]{6}$/.test(value);
}
```

それから、その新しい matcher を使うために、`src/routes/colors/[color]` を `src/routes/colors/[color=hex]` にリネームしてください。

これで、誰かがこのルート(route)に移動してきたときはいつでも、SvelteKit が `color` が有効な `hex` value か検証します。違った場合、SvelteKit は、他のルート(routes)にマッチするか試行し、どれにもマッチしない場合は最終的に 404 を返します。

> [!NOTE] Matcher はサーバーとブラウザの両方で動作します。
