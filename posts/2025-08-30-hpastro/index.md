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