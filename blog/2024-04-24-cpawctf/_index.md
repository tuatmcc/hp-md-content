---
title: CpawCTF カンニングシート
date: "2024-04-24"
author: sugawa
---

# はじめに

部内 CTF 初心者会用に作った CpawCTF 2024 のカンニングシートです。

# Level 1

## Q1.[Misc] Test Problem

以下のフラグを提出すれば正解です。

```title="flag"
cpaw{this_is_Cpaw_CTF}
```

## Q6.[Crypto] Classical Cipher

シーザー暗号です。3文字面しただけなので、 -3 すれば解読できます。[ASCII コード表](https://www.tuatmcc.com/blog/2024-01-26-ascii-table/)を見たらわかりやすいと思います。

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char flag[] = "fsdz{Fdhvdu_flskhu_lv_fodvvlfdo_flskhu}";
    int n = strlen(flag);
    for(int i = 0; i < n; i++){
        if (('A' <= flag[i] && flag[i] <= 'Z')
            || ('a' <= flag[i] && flag[i] <= 'z')){
            flag[i] -= 3;
        }
    }
    printf("%s", flag);
}
```

<details>
<summary>フラグ</summary>

```title="flag"
cpaw{Caesar_cipher_is_classical_cipher}
```

</details>

ここでアルファベットだけ選んでますが、シーザー暗号になってるのがアルファベットだけなので、これで問題ないです。

```c
('A' <= flag[i] && flag[i] <= 'Z')
          || ('a' <= flag[i] && flag[i] <= 'z')
```

アルファベット以外もやるとこうなります。

```
cpawxCaesar\cipher\is\classical\cipherz
```

## Q7.[Reversing] Can you execute ?

`exec_me` をダウンロードしてください。

はじめになんのバイナリファイルかを調べます。 `file` コマンドを使います。

```bash
file exec_me
```

こんなのが出てきます。

```
exec_me: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 2.6.24, BuildID[sha1]=663a3e0e5a079fddd0de92474688cd6812d3b550, not stripped
```

`ELF` ファイルであることがわかりました。これは Linux の実行ファイルです。実行してみます。

```bash
./exec_me
```

出てきましたね。

<details>
<summary>フラグ</summary>

```
cpaw{Do_you_know_ELF_file?}
```

</details>

## Q8.[Misc] Can you open this file ?

`file` コマンドを使います。

```bash
file open_me
```

```
open_me: Composite Document File V2 Document, Little Endian, Os: Windows, Version 10.0, Code page: 932, Author: v, Template: Normal.dotm, Last Saved By: v, Revision Number: 1, Name of Creating Application: Microsoft Office Word, Total Editing Time: 28:00, Create Time/Date: Mon Oct 12 04:27:00 2015, Last Saved Time/Date: Mon Oct 12 04:55:00 2015, Number of Pages: 1, Number of Words: 3, Number of Characters: 23, Security: 0
```

`Document` ファイルのようです。 `Name of Creating Application: Microsoft Office Word` って書いてあるのでこのファイルは `Word` で作られたようです。

Word で開いてみましょう。

<details>
<summary>フラグ</summary>

![Q8-1.png](Q8-1.png)

```
cpaw{Th1s_f1le_c0uld_be_0p3n3d}
```

</details>

## Q9.[Web] HTML Page

ページを開きましょう。右クリックか、 `F12` を押して開発者ツールを開いてください。

`ctr+F` を押してページエレメントを `cpaw{` で検索すると出てきます。

<details>
<summary>フラグ</summary>

![Q9-1.png](Q9-1.png)

```
cpaw{9216ddf84851f15a46662eb04759d2bebacac666}
```

</details>

## Q10.[Forensics] River

写真のメタ情報を読む問題です。 [こちら](http://exif-check.org/)のサイトで読むことができます。

![Q10-1.png](Q10-1.png)

<details>
<summary>フラグ</summary>

甲突川(こうつきがわ)って言うらしい。

```
cpaw{koutsukigawa}
```

</details>

## Q11.[Network]pcap

`pcap` はパケットキャプチャファイルです。 `Wireshark` などのツールで開くことができます。

[Wireshark のダウンロード](https://www.wireshark.org/download.html)

<details>
<summary>フラグ</summary>

![Q11-1.png](Q11-1.png)

```
cpaw{gochi_usa_kami}
```

ごちうさ神！

</details>

## Q12.[Crypto]HashHashHash

ハッシュ関数は、任意の長さのデータを固定長のデータに変換する関数です。ハッシュ関数は、同じデータに対しては必ず同じハッシュ値を返し、異なるデータに対しては異なるハッシュ値を返します。

今回は SHA-1 という種類のハッシュ関数です。

あるハッシュ値をググったりすると、ハッシュ値と元のデータのテーブルを持っているサイトが出てくるので、それを使って解読することができます。

<details>
<summary>フラグ</summary>

[こーゆうサイト](https://md5hashing.net/hash/sha1/e4c6bced9edff99746401bd077afa92860f83de3)を使って解読してみましょう。

```
cpaw{Shal}
```

</details>

## Q14.[PPC]並べ替えろ

ソートするプログラムを書きましょう。

<details>
<summary>フラグ</summary>

```c
#include <stdio.h>
#include <stdlib.h>

int cmpfunc(const void *a, const void *b)
{
 return (*(int *)b - *(int *)a);
}

int main()
{
 int ciphertext[] = {15, 1, 93, 52, 66, 31, 87, 0, 42, 77, 46, 24, 99, 10, 19, 36, 27, 4, 58, 76, 2, 81, 50, 102, 33, 94, 20, 14, 80, 82, 49, 41, 12, 143, 121, 7, 111, 100, 60, 55, 108, 34, 150, 103, 109, 130, 25, 54, 57, 159, 136, 110, 3, 167, 119, 72, 18, 151, 105, 171, 160, 144, 85, 201, 193, 188, 190, 146, 210, 211, 63, 207};
 int n = sizeof(ciphertext) / sizeof(ciphertext[0]);
 qsort(ciphertext, n, sizeof(int), cmpfunc);
 for (int i = 0; i < n; i++)
 {
  printf("%d", ciphertext[i]);
 }
 return 0;
}
```

```
cpaw{2112102072011931901881711671601591511501461441431361301211191111101091081051031021009994938785828180777672666360585755545250494642413634333127252420191815141210743210}
```

</details>

# Level 2

## Q13.[Stego]隠されたフラグ

モールス信号です。[こーゆうサイト](https://morsedecoder.com/ja/)を使うとできます。

<details>
<summary>フラグ</summary>

```
cpaw{hidden_message:)}
```

</details>

## Q15.[Web] Redirect

`http://q15.ctf.cpaw.site/` にアクセスすると `http://q9.ctf.cpaw.site/` にリダイレクトされます。ブラウザの拡張機能で `http://q15.ctf.cpaw.site/` にアクセスしたときの通信データを見てみましょう。 `ログを保持` や `Preserve log` をオンにしてください。

<details>
<summary>フラグ</summary>

`http://q15.ctf.cpaw.site/` にアクセスしたときのレスポンスヘッダーにフラグがあります。

![Q15-1.png](Q15-1.png)

```
cpaw{4re_y0u_1ook1ng_http_h3ader?}
```

</details>

## Q16.[Network+Forensic]HTTP Traffic

WireShark で開いてみましょう。そして WireShark で通信してるファイルを復元します。ファイル → オブジェクトをエクスポート → HTTP で、すべて保存してください。

![Q16-1.png](Q16-1.png)

`network100` ダミーか、、、

`network100(1).html` にして、ブラウザで開いてみましょう。

![Q16-2.png](Q16-2.png)

![Q16-3.png](Q16-3.png)

うまく表示されない、、、どうやら `bootstrap.css` と `button2.js` がそれぞれ `css` と `js` というフォルダの中にあるようです。フォルダを作って、それぞれのファイルを移動してください。

<details>
<summary>フラグ</summary>

![Q16-4.png](Q16-4.png)

```
cpaw{Y0u_r3st0r3d_7his_p4ge}
```

</details>

## Q17.[Recon]Who am I ?

`@porisuteru スペシャルフォース2` で検索してみましょう。

<details>
<summary>フラグ</summary>

```
cpaw{parock}
```

</details>

# Q18.[Forensic]leaf in forest

`pcap` かと思ったら違いました、、、 先頭 16 byte 以降に `lovelive!` がいっぱい書かれています。たまに大文字や `{}` が入っています。なので、 16 byte 以降で `A-Z` と `{}` と `_` だけを取り出します。

![Q18-1.png](Q18-1.png)

<details>
<summary>フラグ</summary>

```c
#include <stdio.h>
#include <stdlib.h>

char buf[65565];
char result[65565];
int main()
{
    const char path[] = "misc100";
    int index = 0;
    FILE *fp = fopen(path, "r");

    fread(buf, 1, sizeof(buf), fp);
    fclose(fp);

    for (int i = 16; i < sizeof(buf); i++)
    {
        if ('A' <= buf[i] && buf[i] <= 'Z' || buf[i] == '{' || buf[i] == '}' || buf[i] == '_')
            result[index++] = buf[i];
    }

    puts(result);
    return 0;
}
```

```
cpaw{mgrep}
```

</details>

## Q19.[Misc]Image

zip ファイルですが、解凍できません。 `file` コマンドで調べてみましょう。

```
misc100.zip: OpenDocument Drawing
```

どうやら `OpenDocument Drawing` というファイルのようです。  `OpenDocument Drawing` というのは `Word` で開くことができます。 `Word` などのファイルは実態が `zip` であることがよくあります。

<details>
<summary>フラグ</summary>

![Q19-1.png](Q19-1.png)

```
cpaw{It_is_fun__isn't_it?}
```

</details>

## Q20.[Crypto]Block Cipher

ソースコードを見た感じ、コンパイルして引数に暗号文とテキトーな数字を入れるとフラグが出てくるようです。

数字は 1 から順に入れていってみましょう。

<details>
<summary>フラグ</summary>

4 回目で出ました。

```bash
$ ./a.out ruoYced_ehpigniriks_i_llrg_stae 1
cpaw{ruoYced_ehpigniriks_i_llrg_stae}
$ ./a.out ruoYced_ehpigniriks_i_llrg_stae 2
cpaw{urYoec_dheipngriki_s_illgrs_ate}
$ ./a.out ruoYced_ehpigniriks_i_llrg_stae 3
cpaw{ourecYe_diphingkiri_sll__grats}
$ ./a.out ruoYced_ehpigniriks_i_llrg_stae 4
cpaw{Your_deciphering_skill_is_great}
```

```
cpaw{Your_deciphering_skill_is_great}
```

</details>

## Q21.[Reversing]reversing easy

普通に実行すると `cpaw{}` だけが出てきます。 `gdb` を使って中のアセンブリを見てみます。以下のコマンドで起動します。

```bash
gdb rev100
```

main 関数のアセンブリを見てみます。

```
(gdb) disas main
```

```
Dump of assembler code for function main:
   0x0804849d <+0>:     push   %ebp
   0x0804849e <+1>:     mov    %esp,%ebp
   0x080484a0 <+3>:     and    $0xfffffff0,%esp
   0x080484a3 <+6>:     sub    $0x50,%esp
   0x080484a6 <+9>:     mov    %gs:0x14,%eax
   0x080484ac <+15>:    mov    %eax,0x4c(%esp)
   0x080484b0 <+19>:    xor    %eax,%eax
   0x080484b2 <+21>:    movl   $0x77617063,0x46(%esp)
   0x080484ba <+29>:    movw   $0x7b,0x4a(%esp)
   0x080484c1 <+36>:    movl   $0x79,0x20(%esp)
   0x080484c9 <+44>:    movl   $0x61,0x24(%esp)
   0x080484d1 <+52>:    movl   $0x6b,0x28(%esp)
   0x080484d9 <+60>:    movl   $0x69,0x2c(%esp)
   0x080484e1 <+68>:    movl   $0x6e,0x30(%esp)
   0x080484e9 <+76>:    movl   $0x69,0x34(%esp)
   0x080484f1 <+84>:    movl   $0x6b,0x38(%esp)
   0x080484f9 <+92>:    movl   $0x75,0x3c(%esp)
   0x08048501 <+100>:   movl   $0x21,0x40(%esp)
   0x08048509 <+108>:   movw   $0xa7d,0x15(%esp)
   0x08048510 <+115>:   movb   $0x0,0x17(%esp)
   0x08048515 <+120>:   movl   $0x5,0x1c(%esp)
   0x0804851d <+128>:   lea    0x46(%esp),%eax
   0x08048521 <+132>:   mov    %eax,0x4(%esp)
   0x08048525 <+136>:   movl   $0x8048620,(%esp)
   0x0804852c <+143>:   call   0x8048350 <printf@plt>
   0x08048531 <+148>:   cmpl   $0x5,0x1c(%esp)
   0x08048536 <+153>:   je     0x804855e <main+193>
   0x08048538 <+155>:   movl   $0x0,0x18(%esp)
   0x08048540 <+163>:   jmp    0x8048557 <main+186>
   0x08048542 <+165>:   mov    0x18(%esp),%eax
   0x08048546 <+169>:   mov    0x20(%esp,%eax,4),%eax
   0x0804854a <+173>:   mov    %eax,(%esp)
   0x0804854d <+176>:   call   0x8048390 <putchar@plt>
   0x08048552 <+181>:   addl   $0x1,0x18(%esp)
   0x08048557 <+186>:   cmpl   $0x8,0x18(%esp)
   0x0804855c <+191>:   jle    0x8048542 <main+165>
   0x0804855e <+193>:   lea    0x15(%esp),%eax
   0x08048562 <+197>:   mov    %eax,0x4(%esp)
   0x08048566 <+201>:   movl   $0x8048620,(%esp)
   0x0804856d <+208>:   call   0x8048350 <printf@plt>
   0x08048572 <+213>:   mov    $0x0,%eax
   0x08048577 <+218>:   mov    0x4c(%esp),%edx
   0x0804857b <+222>:   xor    %gs:0x14,%edx
   0x08048582 <+229>:   je     0x8048589 <main+236>
   0x08048584 <+231>:   call   0x8048360 <__stack_chk_fail@plt>
   0x08048589 <+236>:   leave  
   0x0804858a <+237>:   ret    
End of assembler dump.
```

`0x080484b2` で `0x46(%esp)` に `$0x77617063` を代入しています。[アスキーコード表](https://tuatmcc.com/blog/2024-01-26-ascii-table/)を見ると `wapc` になります。 リトルエンディアンなので逆になっているので、 `cpaw` であることがわかります。 このことから `0x080484b2` から `0x08048515` で `mov` を使っているので、プラグのテキストを代入していると推測できます。

`0x0804851d` から `0x0804852c` は `printf` を呼び出しています。

`0x08048531` で `0x1c(%esp)` と数字の `5` を比較して、 `0x08048536` で等しければ `0x804855e` にジャンプします。 `0x1c(%esp)` ですが、 `0x08048515` で `5` を代入してから変更をしていないので、必ず `0x804855e` にジャンプします。

`0x0804855e` から `0x0804856d` は `printf` を呼び出しています。

`0x08048572` 以降は main 関数の終了処理です。

`0x08048536` で必ずジャンプしてしまうため、 `0x08048538` から `0x0804855c` の間にフラグを出力する処理があると推測します。そのため、 `0x08048531` を処理する直前に `0x1c(%esp)` に `5` 以外の数字を代入して、 `0x08048536` でジャンプしないようにします。

`0x08048531` にブレークポイントを刺します。

```
(gdb) break *0x08048531
```

`r` で実行します。

```
(gdb) r
```

`0x08048531` で停止します。 `disass` でアセンブリを見て見ましょう。矢印で指しているところが今の命令です。

```
(gdb) disass
Dump of assembler code for function main:
   0x0804849d <+0>:     push   %ebp
   0x0804849e <+1>:     mov    %esp,%ebp
   0x080484a0 <+3>:     and    $0xfffffff0,%esp
   0x080484a3 <+6>:     sub    $0x50,%esp

   ***** 省略 *****

   0x08048515 <+120>:   movl   $0x5,0x1c(%esp)
   0x0804851d <+128>:   lea    0x46(%esp),%eax
   0x08048521 <+132>:   mov    %eax,0x4(%esp)
   0x08048525 <+136>:   movl   $0x8048620,(%esp)
   0x0804852c <+143>:   call   0x8048350 <printf@plt>
=> 0x08048531 <+148>:   cmpl   $0x5,0x1c(%esp)
   0x08048536 <+153>:   je     0x804855e <main+193>
   0x08048538 <+155>:   movl   $0x0,0x18(%esp)
   0x08048540 <+163>:   jmp    0x8048557 <main+186>
   
   ***** 省略 *****
```

`0x1c(%esp)` に `5` 以外の数字を代入します。ここでは `0x1c(%esp)` に `0` を代入します。

```
(gdb) p *(int*)($esp + 0x1c) = 0
```

`c` で続行します。

```
(gdb) c
```

<details>
<summary>フラグ</summary>

```
cpaw{yakiniku!}
```

</details>

## Q22.[Web]Baby's SQLi - Stage 1-

`palloc_home` テーブルを表示する SQL を書きましょう。

```
select * from palloc_home;
```

<details>
<summary>フラグ</summary>

```
cpaw{palloc_escape_from_stage1;(}
```

</details>

<details>
<summary>フラグ</summary>

</details>
