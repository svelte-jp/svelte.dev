# svelte-jp/svelte.dev への貢献について

svelte-jp/svelte.dev はSvelte公式ドキュメントサイトの日本語化プロジェクトです。

このリポジトリは[sveltejs/svelte.dev](https://github.com/sveltejs/svelte.dev)をフォークして作成されており、ライセンスやコミュニティ・コラボレーションの精神についてはSvelte本体のそれを引き継ぎます。

Svelte公式のCONTRIBUTING.mdはこちらです、是非ご一読ください。

- [CONTRIBUTING.md - sveltejs/svelte](https://github.com/sveltejs/svelte/blob/main/CONTRIBUTING.md)


## 貢献するには

貢献する方法はたくさんあり、その多くはコードを書く必要もなければ、いきなり翻訳する必要もありません。

- 日本語ドキュメントサイト([https://svelte.jp/](https://svelte.jp/))を使ってみてください。気になるところや改善点があれば[Issueを開いて](#issueを作成する)お知らせください。
- 翻訳で貢献されたい場合は[翻訳作業について](#翻訳作業について)をチェックしてみてください。翻訳にはみなさんの協力が必要です。誤訳があっても誤字・脱字があっても単語が統一できていなくても構いません、後からみんなで良くしていければと考えています。

貢献は大歓迎です！もし貢献を迷っていたり、貢献に助けが必要であれば[Svelte日本のDiscord](https://discord.com/invite/YTXq3ZtBbx)で知らせてください。


## ディレクトリ構成・翻訳の仕組み

ドキュメントのファイルはこのリポジトリの [`apps/svelte.dev/content`](https://github.com/svelte-jp/svelte.dev/tree/main/apps/svelte.dev/content) ディレクトリにあります。

- **blog**
  - Blogは apps/svelte.dev/content/blog 配下にあります。  
- **docs**
  - Docsは apps/svelte.dev/content/docs 配下にあります。CLI、SvelteKit、Svelte本体のドキュメントがそれぞれディレクトリで分かれています。
    - cli: CLI ツールのドキュメントがあります。
	- kit: SvelteKit のドキュメントがあります。
	- svelte: Svelte のドキュメントがあります
- **tutorial**
  - tutorial は apps/svelte.dev/content/tutorial 配下のそれぞれの章ごとに `index.md` というファイルがあります。

```
apps/svelte.dev/content
├── blog
│   ├── 2016-11-26-frameworks-without-the-framework.md  # <- blog
│   ...
│
├── docs
│   ├── cli
│   │   ├── 10-introduction
│   │   │   ├── 10-overview.md  # <- CLI のドキュメント
│   │   │   ...
│   │   ...
│   │   
│   ├── kit
│   │   ├── 10-getting-started
│   │   │   ├── 10-introduction.md  # <- SvelteKit のドキュメント
│   │   │   ...
│   │   ...
│   │
│   ├── svelte
│   │   ├── 01-introduction
│   │   │   ├── 01-introduction.md  # <- Svelte のドキュメント
│   │   │   ...
│   │   ...
│   ...
│
├── examples
│
└── tutorial
    ├── 01-svelte
    │   ├── 01-introduction
    │   │   ├── 01-welcome-to-svelte
    │   │   │   ├── +assets...
    │   │   │   └── index.md         # <- tutorial
    │   │   ...
    │   ...
	...
```

サイトのソース、TOPページの日本語訳は [apps/svelte.dev/src](https://github.com/svelte-jp/svelte.dev/tree/main/apps/svelte.dev/src) にあります。


## 翻訳の流れ

### 1. 翻訳するドキュメントを選ぶ

翻訳が必要な文書は[issue](https://github.com/svelte-jp/svelte.dev/issues?q=is%3Aopen+is%3Aissue)が作成されています。

まだ誰も着手していないIssueには`翻訳者募集中`というLabelがついています。翻訳したいものがあれば、Issueのコメントで知らせてください(堅苦しい挨拶などは不要です。「この翻訳やりましょうか？」と言っていただけたらそれだけでとても嬉しいです！)。

運営側から依頼する旨をコメントで返信しますので、その後に作業を開始してください。

もし翻訳したいドキュメントのIssueがなければ、Issueを作成してください。


### 2. 翻訳作業

このリポジトリをForkし、ローカルにcloneしてください。

```
git clone https://github.com/{USER}/svelte.dev.git
```

[ディレクトリ構成・翻訳の仕組み](#ディレクトリ構成翻訳の仕組み)を参考に、担当する文書を見つけてください。

実際の翻訳については[翻訳のガイドライン](#翻訳のガイドライン)を参考にしてください。

> いきなり完璧な翻訳を目指さなくても大丈夫です。PRに間違いや誤字・脱字があっても大丈夫です。ちゃんとレビューをしますし、レビューで怒ったりしませんのでご安心ください。それより、あなたがこのプロジェクトに貢献するため時間と労力を割いてくれたことに感謝しかありません。


#### 2-1. 見出しの翻訳について

マークダウンでは、行の先頭に `#` が付けられた行は見出し要素になります。
この見出し要素には自動で id が割り付けられ、ページ内の特定の位置にフォーカスさせることができるようになっています。

例えば、以下のようなマークダウンの場合...

```markdown
## Alternatives to SvelteKit
```

...以下のような HTML に変換されます。

```html
<h2 id="Alternatives-to-SvelteKit">
  <span>Alternatives to SvelteKit</span>
  <a href="#Alternatives-to-SvelteKit" class="permalink" aria-label="permalink"></a>
</h2>
```

この自動で id を割り振る仕組みは、マルチバイト文字に対応していません。
また、もし対応していたとしても、本来割り振られる id とは異なるものになってしまいます。
それを防ぐため、見出しの翻訳をする場合は、HTML のコメント要素を使用して id を指定します。

```markdown
## SvelteKit の代替手段 <!--Alternatives-to-SvelteKit-->
```

こうすると、以下のような HTML に変換されるようになります。

```html
<h2 id="Alternatives-to-SvelteKit">
  <span>SvelteKit の代替手段</span>
  <a href="#Alternatives-to-SvelteKit" class="permalink" aria-label="permalink"></a>
</h2>
```

実際のソースはこちら:
https://github.com/svelte-jp/svelte.dev/blob/0f7d41d94f1a67036b736ddcabb00f9c24850ba2/apps/svelte.dev/content/docs/svelte/01-introduction/02-getting-started.md?plain=1#L17

### 3. lintの実行

※現在 lint は調整中ですので、無視して先に進めてください。


### 4. Pull Request作成

Fork元にPull Requestを提出してください。Pull RequestのコメントにはIssueの番号を含めてください。レビュー後、問題がなければマージされます。
PRに間違いや誤字・脱字、ガイドライン違反があっても大丈夫です。間違いを恐れないでください。


### 文体

「だである」ではなく「ですます」調を使用してください。


### 改行位置を原文と揃える

可能な限り、原文と翻訳文の行数を揃え、更新時のdiffチェックが楽になるように協力してください。


### 単語、表記ゆれ

※単語、表記揺れについては現在準備中ですので、無視して先に進めてください。


### ダッシュ

原文で使われているダッシュは、以下のように場合に応じて訳し分けてください。

- 和訳で文中に埋め込まれるような語句を区切っている場合、ダッシュの代わりに括弧でその語句を囲んでください
- 和訳で文と文の区切りになっている場合、ダッシュの代わりに句点（`。`）を打ってください
- 箇条書きの項目と説明を区切っている場合、ダッシュをそのままにする


## issueを作成する

何かお気づきの点などがある場合はお気軽にissueを作成して頂いて構いません。
以下のテンプレートを用意しております。

- 翻訳ドキュメント追加
  - 翻訳したい/してほしいドキュメントがissueになければこちらをご使用ください。
- 誤字・脱字・誤訳報告、翻訳改善要望
  - 誤字・脱字・誤訳や、不自然な言い回しやよりより翻訳文があればこちらをご使用ください。
- その他
  - ご質問、ご意見、お気軽にどうぞ！


## その他

- Svelte本体の変更は大体月に1度のペースで日本語サイトにも反映を行います。これは、Svelte本体のサイトが大体月に1度(月初、毎月のNewsletterが入るタイミング)で更新されるためです。
  Svelte本体のサイトに緊急で更新がある場合はなるべくそれに追従したいと考えています。


## 備考

翻訳の進め方やCONTRIBUTING.mdに記載する内容などは、各フロントエンドフレームワーク及びライブラリの日本語化プロジェクトである、[angular/angular-ja](https://github.com/angular/angular-ja)、[vuejs/jp.vuejs.org](https://github.com/vuejs/jp.vuejs.org), [reactjs/ja.reactjs.org](https://github.com/reactjs/ja.reactjs.org)を参考にさせて頂きました。
