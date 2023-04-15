---
title: Git・GitHub講習
date: 2023-04-15
author: ojii3
---

# はじめに

皆さんこんにちは。今日はGit・GitHubの使い方について学びましょう。
Git・GitHubは、ソフトウェアの開発に必須級のツールで、世界中で利用されています。

Gitは自分のPCにインストールして使うツールですが、GitHubはGitを使う人たち向けのWEB上のサービスです。

GitHubと同様なものとして、GitLabやBitBacketなどがあります(使いません)

混同しないようにしましょう。

# 準備編

WSL環境を前提とします。

## Gitのインストール

Gitを使うには、まずGitをインストールする必要があります。以下の手順でインストールしましょう。

1. Gitの公式ダウンロードサイト（https://git-scm.com/downloads）にアクセスします。
2. 今回はWSLにインストールするので、Linux/Unix → Ubuntu のインストール方法を確認します。
3. WSLを開き、指示にしたがってコマンドを実行します。コマンドの先頭に`sudo`権限を付与しましょう。以下のようなコマンドを実行することになるはずです。

```shell: bash
sudo  add-apt-repository ppa:git-core/ppa
```
```shell: bash
sudo update
```
```shell: bash
sudo  apt install git
```

(ひょっとしてWindows側に入れたほうが良かったりするかな...?)

(必要になったら自分で入れてください。ただし、改行コードのデフォルト設定には注意です。)

## Gitクライアント(GUI)のインストール

コマンドを覚えるのは大変なので、とりあえずGUIでGitを使えるようになりましょう。

1. 様々なツールがあります。公式がまとめているサイト(https://git-scm.com/download/gui/windows)を見てみましょう。
2. 今回はSource Treeをインストールします。Windows側にインストールし、Windows側からWSLのディレクトリにアクセスして使います。(Linuxで動かないソフトも使えるのがwslのメリットではありますね...)
3. 使い方がうろ覚えなので、部室PCでみんなといっしょに操作しようと思います...

(VSCodeにビルトインでGUIクライアントがくっついていたりします。IDEには普通にくっついています。)

(VSCodeで教えちゃおうかな...)

## GitHubアカウントの作成

次に、GitHubのアカウントを作成しましょう。

1. GitHubの公式サイト（https://github.com/）にアクセスします。
2. "Sign up"をクリックし、必要事項を入力します。
3. "Create account"をクリックして、アカウントを作成します。

(モバイルアプリ入れておくと通学中とかGitHubサーフィンできるよ。あとモバイル認証用。)

## sshキーの作成と登録

GitHubでは、SSHという通信を使ってGitと通信します。SSHキーを作成し、GitHubに登録しましょう。

1. Git Bashを起動します。
2. ssh-keygenコマンドを実行します。すると、秘密鍵と公開鍵が生成されます。
3. 公開鍵をGitHubに登録します。GitHubの"Settings"→"SSH and GPG keys"から"New SSH key"をクリックし、公開鍵を入力して登録します。タイトルはPCの機種名とOS名あたりでいいんじゃないでしょうか

# 実践編

さて、準備はコレで完了しました。お勉強の時間です。

よく使う基本概念・操作

1. `init`, `stage`, **`commit`**
2. **`clone`**, **`fetch`**, **`pull`**, **`push`**
3. **`branch`**, **`merge`**
4. **`pull request`**

(Pull RequestはGit操作ではなくGitHub独自のシステムですが...)

自分のPC上の操作か、オンライン上での操作かを意識できるようになると良いです。

## Organizationへの参加

これは我々がやることです。Organizationのリポジトリ(`tuatmcc/○○`)を作ったり、開発に参加することができるようになります。

## チーム開発の仕方

今すぐチーム開発をするわけではないので(してもいいけど)、今完璧に覚える必要はありません。

1. GitHubの `New` ボタンから、`GitLecture2023`と言う名前でリポジトリを作成してみましょう。visiblityはpublicで結構です
2. GitHubの `Clone` ボタンから、SSHのURLをコピーしましょう。
3. Gitクライアントから、URLに先ほどコピーしたものを指定し、クローンします。
4. 出来上がったディレクトリ(フォルダー)の中に、`hello.c`というプログラムを作成してください。

使用するプログラムの例

```c :hello.c
#include <stdio.h>

int main() {
    printf("Hello, World!");
    return 0;
}
```

5. 保存したらステージングし、プッシュします。
6. 最初の一人目のプッシュが成功し、リモート(GitHub)が更新されます。(それ以外の人たちのプッシュはちゃんと失敗するはずです)
6. プッシュが通った最初の一人目以外は、一旦書いたプログラムを消してから、プルします。

