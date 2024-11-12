---
title: $env/static/public
---

ブラウザに公開しても安全な環境変数もあります。これらは `PUBLIC_` プレフィックスを付けることで、プライベートな環境変数と区別します。

`.env` にある2つのパブリックな環境変数に値を追加します。

```env
/// file: .env
PUBLIC_THEME_BACKGROUND=+++"steelblue"+++
PUBLIC_THEME_FOREGROUND=+++"bisque"+++
```

そして、これらを `src/routes/+page.svelte` にインポートします。

```svelte
/// file: src/routes/+page.svelte
<script>
---	const PUBLIC_THEME_BACKGROUND = 'white';
	const PUBLIC_THEME_FOREGROUND = 'black';---
+++	import {
		PUBLIC_THEME_BACKGROUND,
		PUBLIC_THEME_FOREGROUND
	} from '$env/static/public';+++
</script>
```
