---
title: ホームページを Astro で作り直した
draft: true
date: 2025-08-30
tags: [dev, web]
---

## 以前のMCCのホームページ

Next.js に Velite.js や next-mdx-remote 等を組み合わせてブログを構成していました。

また、スタイリングには CSS Modules を用いており、一部 Tailwind CSS に移行された状態でした。

## リニューアルのきっかけ

もちろん、前々から様々な理由で改修の必要性は感じていたのですが、決め手は Next.js のバグを踏んだことです。 


Cloudflare Pages から Cloudflare Workers へ移行する際、依存を一通りアップデートしたところ以下の Issue と同様のエラーに遭遇しました。

https://github.com/vercel/next.js/issues/58171

このエラー、静的生成のときだけ起こるようで、例えば OpenNext 等を使うと起こりません。
(注: Cloudflare で Next.js を使用する場合、基本的には静的生成するかOpenNextを使うかの2択です)

というわけで、最近 Astro を気に入っていたのもあり、Next.js をやめました。

## 移行の方針について

最低限の目標は以下の通りでした。

- 中身がほぼ同じな `blog`, `news` を `posts` に統合し、タグで管理する
- 新たに `workshops` カテゴリを生やし、部内の講習資料を Astro Starlight のように作れるようにする

それに伴い、以下の点も意識しました。

- デザインをかっこよくする (僕の趣味ですすみません)
- スタイリングを Tailwind CSS に統一し、デザイントークンの管理を改善する。

## Figma でデザインする

あまりデザインは得意ではなく、すぐCSSで細かいところを書いてしまうのですが、今回は意識してまずは全体のイメージをFigmaに起こすことにしました。