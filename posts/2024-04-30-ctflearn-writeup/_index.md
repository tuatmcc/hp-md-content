---
title: CTF Learn Write Up
date: 2024-04-30
author: sugawa197203
draft: false
---

# はじめに

部内 CTF 初心者会用に作った [CTFLEARN](https://ctflearn.com/) Write Up です。

## Practice Flag

フラクを提出する練習です。

<details>
<summary>Flag</summary>

```titke="flag"
CTFlearn{4m_1_4_r3al_h4ck3r_y3t}
```

</details>

## Basic Injection

SQL Injection の基本的な問題です。コメントの機能がないようです。

```txt
' OR '1' = '1
```

<details>
<summary>Flag</summary>

```title="flag"
CTFlearn{th4t_is_why_you_n33d_to_sanitiz3_inputs}
```

</details>

## Forensics 101

バイナリエディタや `strings` コマンドを使うとフラグが出てきます。

<details>
<summary>Flag</summary>

```title="flag"
flag{wow!_data_is_cool}
```

</details>

## Character Encoding

[アスキーコード表](/posts/2024-01-26-ascii-table/) を見てエンコードしましょう。

<details>
<summary>Flag</summary>

```title="flag"
ABCTF{45C11_15_U53FUL}
```

</details>

## Taking LS

Zip ファイルを解凍して中身を見るとパスワード付きPDFがあります。パスワードは `ThePassword.txt` に書いてあります。

<details>
<summary>Flag</summary>

```title="flag"
ABCTF{T3Rm1n4l_is_C00l}
```

</details>

<details>
<summary>Flag</summary>

</details>
