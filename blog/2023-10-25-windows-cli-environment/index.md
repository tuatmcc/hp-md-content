---
title: 部室PC荒らし行為まとめ
date: "2023-10-30"
author: ojii3
---
環境構築の鬼に、俺はなる！

# 動機

WindowsでLinuxみたいなCLI環境を作りたかった。

私の所有する唯一のPCはArchLinux専用機になってしまったので、部室PCのWindowsをいじり倒すことにした。

# 前提

- Windows11

WSLだと動機を満たせないので、今回のテーマ外とします。

# 基本方針

- PowerShell主体
- CLIで色々インストールする

長くなるのでインストールしたツールの使い方はあまり書きません。軽く紹介するだけです。

以降よく出てくるコマンドとして

```
winget install 〇〇
```

```
scoop install 〇〇
```

があります。どちらも`winget(scoop) search`などで検索できます。

# 事前準備


- PowerShell 7
- Windowsターミナル
- Git for Windows
- 白源フォント
- Ctrl2Caps
- scoop

## PowerShell 7

PowerShell 7はクロスプラットフォームな最新のPowerShell (≠Windows PowerShell)。wingetで。PowerShellが起動時に読み込む設定はDocument\PowerShell\Microsoft.PowerShell_profile.ps1に書きます。

## Windows Terminal

WindowsターミナルはWindows11ならデフォルトで入っています。規定のシェルをPowerShell 7にする。お好みで背景を半透明にどうぞ。

唯一の不満はWindowsに言語を日本語にするとアプリ名が「Terminal」ではなく「ターミナル」になり検索しづらくなること。

## Git for Windows

gitは`winget install git`で。SSH等の設定はよしなにする。

## 白源 (NerdFont)

白源はNerdFont(様々なグリフを表示できる)対応の日本語フォントです。GitHubの最新Releasesからダウンロードしてインストール、Windowsターミナルの規定フォントに設定します。

## Ctrl2Caps

Caps2CtrlはCapsLockをCtrlに変えるツール(PowerToysで上手くいかなかったため)。ググってexeをダウンロード。

## Scoop

`scoop`はWindows版CLIインストーラー。`winget`だけだと不十分なので。以下をPowerShellにて実行。

```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser # Optional: Needed to run a remote script the first time
irm get.scoop.sh | iex
```

# コンパイラ・実行環境・パッケージマネージャー

- `llvm` (C: clangその他)
- `gcc` (C: gcc)
- `rustup` (Rust: cargo, rustcその他)
- `nodejs-lts` (JavaScript, TypeScript)
- `rye` (Python: cpython, pipその他)
- `deno` (TypeScript)
- `Visual C++` (C++)

それぞれ必要になったら入れるという感じで。

ryeとdenoはscoopで入れる。Visual C++ は Visual Studio Installerで。それ以外はwinget。Node.jsを開発用途で使う人は気合いでnodenvから入れるべし。


# TUI

- yazi
- Neovim

両方scoopで入る。

yaziはファイラ。エクスプローラーなしでターミナル住むなら必須級。Windowsターミナルでは画像のプレビューはできない模様。NerdFont使用。

Neovimはターミナル内で起動するエディタ。あとで設定してVSCodeくらい高機能にする。


# リッチな見た目

- starship

シェルのプロンプト(ユーザやカレントディレクトリが表示されるところ)をリッチにする。starshipのデフォルトでもgitのbranchや実行環境のバージョンがわかる様になったりと、大変良い。NerdFont使用。


# その他CLI

- github-cli
- fzf + PSFzf
- ripgrep
- unar

## GitHub CLI

`gh`コマンドでターミナルからGitHubの操作ができる。プルリクの作成、マージが特に便利。GitHubの認証の設定もよしなにやってくれる。

## fzf & PSFzf

両方`scoop`でいれる。

fzfはファジーファインダーで、色々なものを曖昧検索できる。少くともエクスプローラーの検索よりは断然速い。他にツールに組み込まれることが多い。

一番のおすすめはシェルのコマンド履歴検索の拡張。PowerShellの設定に

```powershell
Set-PsFzfOption -PSReadlineChordProvider 'Ctrl+t' - PSReadlineChordReverseHistory 'Ctrl+r'
```

を追記。これで`Ctrl + r`が強力になる。

## RipGrep

ripgrepはrust製の多機能で高速なgrep。他のもののと合わせて便利に使える。`yazi`や`Neovim`でも使う。

## unar

unarはunarchiverの略で、(圧縮)ファイル解凍ツール。zipだろうがtarだろうがgzだろうが7zipだろうが問答無用で解凍してくれる。

# Neovimの設定

つらいところ。あとで書く。


# その他の荒らし行為

- Windows10からWindows11にアップグレードした。
- デスクトップやタスクバーのものを消した(自重して一部は残した)。
- Weztermを入れてデフォルトでwslのbashが起動する様にした。
- Chrome拡張にVimiumを入れた。


余裕があったら少しずつ追記・変更するかも。
