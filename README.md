# Homepage Markdown Content

[ホームページ](https://www.tuatmcc.com)に載せるためのマークダウン記事を置いておくリポジトリです。

ホームページのソースコードは[こちら](https://github.com/tuatmcc/homepage2.0)。

- `news`: お知らせ
  - `各お知らせの詳細`
    - `index.md`
    - 画像など
- `blog`: ブログ
  - `お知らせ以外の記事`
    - `index.md`
    - 画像など

## How to use

1. `Add File`ボタンを押し、記事を作成します。
2. `Commit Changes`からファイルを保存(`commit`+`push`)します。
3. 5分以内にホームページに反映されます

ファイル名を`index.md`以外(`_index.md`)以外にすることで下書き状態で保存できます。フォルダ名に日付が入ってるのはパット見のわかりやすさと、GitHub上の表示のソートのためです。

## System

文書保存用リポジトリを分けたことで、ホームページのシステムの影響を受けにくくなりました。

ビルド時にこのリポジトリをクローンしています。
