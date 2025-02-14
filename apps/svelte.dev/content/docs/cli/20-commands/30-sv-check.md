---
NOTE: do not edit this file, it is generated in apps/svelte.dev/scripts/sync-docs/index.ts
title: sv check
---

`sv check`は、プロジェクト内の次のようなエラーや警告を見つけます：

- 未使用のCSS
- アクセシビリティのヒント
- JavaScript/TypeScriptコンパイラエラー

Node 16以降が必要です。

## インストール <!--Installation-->

プロジェクトに`svelte-check`パッケージをインストールする必要があります：

```bash
npm i -D svelte-check
```

## 使用方法 <!--Usage-->

```bash
npx sv check
```

## オプション <!--Options-->

### `--workspace <path>`

ワークスペースへのパス。`node_modules`と`--ignore`で指定したディレクトリ以外のすべてのサブディレクトリがチェックされます。

### `--output <format>`

エラーや警告の表示方法。詳細は[機械可読出力](#Machine-readable-output)を参照してください。

- `human`
- `human-verbose`
- `machine`
- `machine-verbose`

### `--watch`

プロセスを生存させ、変更を監視します。

### `--preserveWatchOutput`

ウォッチモードで画面がクリアされるのを防ぎます。

### `--tsconfig <path>`

`tsconfig`または`jsconfig`ファイルへのパスを指定します。パスはワークスペースパスからの相対パスまたは絶対パスにすることができます。これを行うことで、設定ファイルの`files`/`include`/`exclude`パターンに一致したファイルのみに診断が適用されます。また、TypeScript および JavaScript ファイルからのエラーが報告されます。指定されていない場合は、プロジェクトディレクトリから上方に`jsconfig`/`tsconfig.json`ファイルを探します。

### `--no-tsconfig`

現在のディレクトリとその下にあるSvelteファイルのみをチェックし、`.js`/`.ts`ファイルを無視したい場合に使用します（型チェックされません）。

### `--ignore <paths>`

ワークスペースのルートから相対的に無視するファイルやフォルダ。パスはカンマで区切り、引用符で囲む必要があります。例：

```bash
npx sv check --ignore "dist,build"
```

<!-- TODO what the hell does this mean? is it possible to use --tsconfig AND --no-tsconfig? if so what would THAT mean? -->

`--no-tsconfig`と併用した場合にのみ効果があります。`--tsconfig`と併用した場合、診断されるファイルではなくウォッチされたファイルにのみ影響します。その診断は`tsconfig.json`によって決定されます。

### `--fail-on-warnings`

指定された場合、警告があると`sv check`はエラーコードで終了します。

### `--compiler-warnings <warnings>`

`code`が[コンパイラ警告コード](../svelte/compiler-warnings)で、`behaviour`が`ignore`または`error`である`code:behaviour`ペアのリスト。例：

```bash
npx sv check --compiler-warnings "css_unused_selector:ignore,a11y_missing_attribute:error"
```

### `--diagnostic-sources <sources>`

コード診断を実行するソースのリストをカンマで区切って引用符で囲みます。デフォルトではすべてアクティブです：

<!-- TODO would be nice to have a clearer definition of what these are -->
- `js` (TypeScriptを含む)
- `svelte`
- `css`

例：

```bash
npx sv check --diagnostic-sources "js,svelte"
```

### `--threshold <level>`

診断をフィルタリングします：

- `warning` (デフォルト) — エラーと警告の両方が表示されます
- `error` — エラーのみが表示されます

## トラブルシューティング <!--Troubleshooting-->

プリプロセッサのセットアップやその他のトラブルシューティングについては、[言語ツールのドキュメント](https://github.com/sveltejs/language-tools/blob/master/docs/README.md)を参照してください。

## マシンリーダブル向け出力 <!--Machine-readable-output-->

`--output`を`machine`または`machine-verbose`に設定すると、CIパイプライン内やコード品質チェックなどで機械によって読みやすい形式で出力がフォーマットされます。

各行は新しいレコードに対応しています。行は一つのスペース文字で区切られた列で構成されます。各行の最初の列はミリ秒のタイムスタンプを含み、モニタリング目的で使用できます。第二列は"行タイプ"を示し、それに基づいて後続の列の数とタイプが異なる場合があります。

最初の行は`START`タイプで、ワークスペースフォルダを含みます（引用符で囲まれています）。例：

```
1590680325583 START "/home/user/language-tools/packages/language-server/test/plugins/typescript/testfiles"
```

`ERROR`または`WARNING`レコードが続く場合があります。それらの構造は出力の引数によって異なります。

引数が`machine`の場合、ファイル名、開始行および列番号、エラーメッセージが示されます。ファイル名はワークスペースディレクトリ相対です。ファイル名とメッセージはどちらも引用符で囲まれています。例：

```
1590680326283 ERROR "codeactions.svelte" 1:16 "Cannot find module 'blubb' or its corresponding type declarations."
1590680326778 WARNING "imported-file.svelte" 0:37 "Component has unused export property 'prop'. If it is for external reference only, please consider using `export const prop`"
```

引数が`machine-verbose`の場合、ファイル名、開始行と列番号、終了行と列番号、エラーメッセージ、診断コード、コードの人間が読みやすい説明、診断の人間が読みやすいソース（例：svelte/typescript）が示されます。ファイル名はワークスペースディレクトリ相対です。各診断はタイムスタンプでプレフィックスされた[ndjson](https://en.wikipedia.org/wiki/JSON_streaming#Newline-Delimited_JSON)行として表されます。例：

```
1590680326283 {"type":"ERROR","fn":"codeaction.svelte","start":{"line":1,"character":16},"end":{"line":1,"character":23},"message":"Cannot find module 'blubb' or its corresponding type declarations.","code":2307,"source":"js"}
1590680326778 {"type":"WARNING","filename":"imported-file.svelte","start":{"line":0,"character":37},"end":{"line":0,"character":51},"message":"Component has unused export property 'prop'. If it is for external reference only, please consider using `export
const prop`","code":"unused-export-let","source":"svelte"}
```

出力は、チェック中に遭遇したファイル、エラー、および警告の合計数を要約する`COMPLETED`メッセージで終了します。例：

```
1590680326807 COMPLETED 20 FILES 21 ERRORS 1 WARNINGS 3 FILES_WITH_PROBLEMS
```

ランタイムエラーが発生した場合、このエラーは`FAILURE`レコードとして表示されます。例：

```
1590680328921 FAILURE "Connection closed"
```

## クレジット <!--Credits-->

- `svelte-check`の基礎を築いたVueの[VTI](https://github.com/vuejs/vetur/tree/master/vti)

## よくある質問 (FAQ) <!--FAQ-->

### なぜ特定のファイル（たとえばステージングされたファイルのみ）をチェックするオプションがないのですか？ <!--FAQ-Why-is-there-no-option-to-only-check-specific-files-(for-example-only-staged-files)-->

`svelte-check`は、チェックが有効になるためにプロジェクト全体を「見る」必要があります。例えば、コンポーネントプロパティの名前を変更しましたが、そのプロパティが使用されている場所の更新を忘れた場合、使用サイトはすべてエラーになりますが、変更されたファイルのみをチェックするとこれらを見逃すことになります。
