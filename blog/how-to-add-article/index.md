---
title: "記事の書き方"
description: "Markdown記事をホームページに追加する方法を説明します。"
date: "2023-01-05"
tags: ["web", "dev"]
img: "https://user-images.githubusercontent.com/84656786/219551946-1b80cbaa-7e2f-47be-a99c-ed9a1a615947.png"
---

# 手順

<https://github.com/tuatmcc/markdown-articles> を更新することがメイン工程となります。

ここから先は、ブラウザからの操作を想定して説明します。クローンしたローカル環境や、スマホアプリ上でも手順は大きくは変わりません。(スマホアプリ上からは一部機能が使えませんので、最終的にはブラウザが必要です)

MCCからのお知らせ記事(活動報告も含む)は、`news`フォルダに、それ以外(技術記事・ポエムなど)は`blog`フォルダにおきます。

例えば、「ホームページリニューアル」というお知らせ記事を作成する手順は以下のようになります。

1. <https://github.com/tuatmcc/markdown-articles> にアクセスし、`news`フォルダに進みます。
2. ページ右上の`Creat new file`を押すと、ブラウザ上で簡易エディタが開くので、ファイル名を`homepage-renewal/index.md`などとして下さい。 **スラッシュ/以降は必ず`index.md`です**
3. マークダウンで記事を書きます。その際の書き方は後ほど述べます。
4. `main`ブランチに`commit`して保存します。
5. (未実装機能です) `Actions`タブを開き、`workflow`から`Deploy`を選択。`Run workflow`を押し、手動でGitHub Actionsを実行すると、ホームページが更新されます。

## 注意事項

記事の先頭に以下のような記述が必要です。

```markdown title="blog/bocchi-the-rock/index.md"
---
title: "ぼっち・ざ・ろっくを鑑賞しました"
description: "ぼっち・ざ・ろっくをみた"
img: "./bocchi-the-rock.webp"
date: "2023-01-03"
tags: [dev, web, nextjs]
author: "Goto Hitori"
---
```

`title`は必須です。`date`も記事並べ替えのために書いてください。

なんらかのブランチからプルリクエストをお願いします。GitHub 上からでもかまいません。この辺はいずれ整

また、画像のURLは、同じフォルダに画像をアップロードし、`./画像のファイル名`とするか、`httpsから始まる外部URL`でお願いします。

なお、ブラウザ上から編集する際は、簡単に画像を置くことができます。

```markdown
![alt text](./bocchi.webp)
```

![alt text](./bocchi.webp)

```markdown
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

### h3~は文字サイズが徐々に小さくなるだけです。h6 まで

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

| title        | date | tags     |
| ------------ | ---- | -------- |
| こんにちは   | 2022 | web, dev |
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
>
> > 引用の中の引用です。
>
> That's all.

## インラインコード

```markdown
`これはインラインコードです` `Font は JetBrains Monoを使用` ``コード内で"`"を使うには、"`"を一個追加してはさみます``
```

`これはインラインコードです` `Font は JetBrains Monoを使用` ``コード内で"`"を使うには、"`"を一個追加してはさみます``

## コードブロック

タイトル(ファイル名)はあってもなくてもいけます。タイトルのみ書くことはできません。

````markdown title="markdown"
```python title="blog.py"
print('Hello World')
```
````

```python title="blog.py"
print('Hello World')
```

````markdown title="markdown"
```diff
- これは削除です
+ これは追加です
```
````

```diff
- これは削除です
+ これは追加です
```

## 数式

KaTex を使用しています。

```math
$$
L = \frac{1}{2} \rho v^2 S C_L
$$
```

$$
L = \frac{1}{2} \rho v^2 S C_L
$$

## emoji

```markdown
:smile: :+1: :tada: :rocket: :metal:
```

:smile: :+1: :tada: :rocket: :metal:
