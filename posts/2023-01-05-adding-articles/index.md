---
title: 記事の書き方
date: 2023-01-05
author: ojii3
tags:
  - web
  - dev
  - blog
img: ./markdown.png
description: Markdown記事をホームページに追加する方法を説明します。
draft: false
---
# 手順

[記事管理用リポジトリ](https://github.com/tuatmcc/hp-md-content) の`main` ブランチにマークダウン記事を追加します。

`posts/`直下に `YYYY-MM-DD-<slug>/`というディレクトリを作成し、その中に`index.md`という名前のマークダウンファイルを作成します。


マークダウンは以下のような形式で書きます。

```markdown
---
title: 記事のタイトル
date: 2023-01-05
author: ojii3
tags: [blog, web, dev]
---

# マークダウンの書き方

![alt text](./markdown.png)
```

前半の `---` で囲まれた部分はメタデータやフロントマターと呼ばれ、記事のタイトルや日付、著者、タグなどを指定します。
`tuatmcc.com/posts/*` では以下のようにフロントマターを定義しています。

```ts
  schema: z.object({
    title: z.string(),
    date: z.date(),
    author: z.string().optional(),
    authors: z.string().array().optional(),
    draft: z.boolean().optional(),
    tags: z.string().array().optional(),
  }),
```



# マークダウンの書き方

マークダウンの書き方を紹介します。基本文法は同じですが、所々他のブログサービスと相違があります。

## 見出し

見出しの右にはリンクがつきます。目次(未実装)とか、ページ内リンクに対応できます。

```markdown
# これは h1 の見出しです

## これは h2 の見出しです

### h3~は文字サイズが徐々に小さくなるだけです。h6 まで
```

# これは h1 の見出しです

## これは h2 の見出しです

### h3\~は文字サイズが徐々に小さくなるだけです。h6 まで

## リスト

箇条書きには`-`, `+`, `*`などが使えます。箇条書きの方はネストできます。

```markdown
- リスト１
- リスト２
  - リスト 2-1
  - リスト 2-2

1. 番号付きリスト 1
2. 番号付きリスト 2
```

- リスト１
- リスト２
- リスト 2-1
- リスト 2-2

1. 番号付きリスト 1
2. 番号付きリスト 2

## チェックボックス

```markdown
- [ ] チェックボックス 1
- [x] チェックボックス 2
```

- [ ] チェックボックス 1
- [x] チェックボックス 2

## 斜体・強調・打消し

`*`,`**`は`_`,`__`と置き換えられます

```markdown
_Italic 斜体です_

**強調**

~~打消し線（css の装飾）~~
```

_Italic 斜体_

**強調**

~~打消し線（css の装飾）~~

## リンク

```markdown
[外部リンク](https://www.google.com)

[内部リンク](/gallery)

生のリンク: <https://google.com>
```

[外部リンク](https://www.google.com)

[内部リンク](/gallery)

生のリンク: <https://google.com>

## 画像

```markdown
外部 URL
![画像](https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png)

内部 URL (相対パス)
![bocchi](./bocchi.webp)
```

外部 URL
![画像](https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png)

内部 URL (相対パス)
![bocchi](./bocchi.webp)

## 折りたたみ

```markdown
<details>
<summary>折りたたみ</summary>

折りたたみの中身です

</details>
```

<details>
<summary>折りたたみ</summary>

折りたたみの中身です

</details>

## 脚注

```markdown
脚注[^1]

[^1]: 脚注です
```

脚注[^1]

[^1]: 脚注です

## 表

```markdown
| title        | date | tags     |
| ------------ | ---- | -------- |
| こんにちは   | 2022 | web, dev |
| これは表です | 2022 | web, dev |
```

| title | date | tags |
| --- | --- | --- |
| こんにちは | 2022 | web, dev |
| これは表です | 2022 | web, dev |

## 引用

```markdown
> 引用です。
>
> > 引用の中の引用です。
>
> That's all.
```

> 引用です。
> >
> > 引用の中の引用です。
> >
> That's all.

## インラインコード

```markdown
`これはインラインコードです` `Font は JetBrains Monoを使用` `` コード内で"`"を使うには、"`"を一個追加してはさみます ``
```

`これはインラインコードです` `Font は JetBrains Monoを使用` `` コード内で"`"を使うには、"\`"を一個追加してはさみます \`\`

## コードブロック

タイトルのみ書くことはできません。

````
```python title="blog.py"
print('Hello World')
```
````

````
```diff lang="python"
print("Hello World")
- print("これは削除です")
+ print("これは追加です")
```
````

````
```python "この単語"
print(この単語をハイライトできます)
```
````

---

```python title="blog.py"
print('Hello World')
```


```diff lang="python"
print("Hello World")
- print("これは削除です")
+ print("これは追加です")
```


```python "この単語"
print(この単語をハイライトできます)
```

特定の単語や行のハイライトなど、その他の機能は[Expressiv Code のドキュメント](https://expressive-code.com/key-features/text-markers/#combining-syntax-highlighting-with-diff-like-syntax)を参照してください。

## 数式

```markdown
$\KaTeX$ を使用しています。

$$
L = \frac{1}{2} \rho v^2 S C_L
$$
```

$\KaTeX$ を使用しています。

$$
L = \frac{1}{2} \rho v^2 S C_L
$$

## 埋め込み

```markdon
<a class="twitter-timeline" href="https://twitter.com/TUATMCC?ref_src=twsrc%5Etfw">Tweets by TUATMCC</a> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
```

<a class="twitter-timeline" href="https://twitter.com/TUATMCC?ref_src=twsrc%5Etfw">Tweets by TUATMCC</a> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
