# Markdown Articles

[ホームページ](https://www.tuatmcc.com)に載せるためのマークダウン記事を置いておくリポジトリです。

ホームページのソースコードは[こちら](https://github.com/tuatmcc/mcc-website)。

- `news`: お知らせ
  - `各お知らせの詳細`
    - `index.md`
    - 画像など
- `blog`: ブログ
  - `お知らせ以外の記事`
    - `index.md`
    - 画像など
- `members`: 部員一覧
  - 各部員のプロフィール


## How to use

**ブランチを気にする必要はありません！ローカル環境・Webブラウザ・モバイルアプリなど、どこからでも編集できます。mainブランチに直コミットしましょう！**

1. `Add File`ボタンを押し、記事を作成します。
2. `main`ブランチにコミットし、保存します。
3. <https://github.com/tuatmcc/mcc-website/actions/workflows/nextjs.yml>にアクセスし、Run workflow`から`main`ブランチを選び実行します。
4. ホームページが更新されます。

## System

文書保存用リポジトリを分けたことで、ホームページのシステムが変わっても文書が影響を受けにくくなりました。

ビルド時にAPIを叩いて記事を取得する代わりに、ビルド時にこのリポジトリをクローンしています。この時、depthオプションを1に設定することで、クローンにかかる時間を短縮していす。
