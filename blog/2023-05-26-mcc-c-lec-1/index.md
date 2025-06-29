---
title: MCC C言語部内講習会 第１回
date: 2023-05-26
author: sugawa197203
tags:
  - dev
description: MCC C言語部内講習会 第１回 を行いました。
draft: false
---
# MCC C 言語部内講習会 第１回

## この講座の対象の人

- MCC 部員
- C 言語を初歩から学びたい人

## 第１回の目次

- [概念編](#概念編)
- [C における変数](#cにおける変数)
    - [変数の型とは](#変数の型とは)
    - [配列とは](#配列とは)
    - [多次元配列](#多次元配列)
- [C における関数](#cにおける関数)
- [C における条件分岐](#cにおける条件分岐)
    - [`if` - `else` 文](#if---else-文)
    - [`switch` - `case` 文](#switch---case-文)
- [C におけるループ(繰り返し)処理](#cにおけるループ繰り返し処理)
    - [`for` 文](#for-文)
    - [`while` 文(`do` \~ `while` 文)](#while-文do--while-文)
    - [`do` \~ `while` 文](#do--while-文)
- [実践編](#実践編)
- [文字の表示](#文字の表示)
    - [演習問題１](#演習問題１)
- [変数の内容の表示](#変数の内容の表示)
    - [演習問題２](#演習問題２)
- [配列の内容の表示](#配列の内容の表示)
    - [演習問題３](#演習問題３)
- [発展編](#発展編)
- [式、文について](#式文について)
- [ポインタ(と配列)](#ポインタと配列)

**この後の内容をチラ見して内容を知っていそうだと判断できる人は次回以降の参加でも大丈夫です！**

## 概念編

### C における変数

C において、変数は主に次の二つの情報を持っています。

- 型
- 値
- (名前)

次に、変数を定義する例を示します。

```c
int i = 0;
```

これは `i` という名前の変数に `0` という値を代入する文です。  
この文から、 `i` について

- `int` 型
- `0` で初期化される

ということが読み取れます。これらの情報はプログラマだけでなくコンパイラにとっても重要です。

#### 変数の型とは

上で述べたように、変数はそれぞれ**型**という情報を持っています。
ここであまり詳しく説明しても理解を妨げるだけなので省略しますが、変数の型についておおむね次のことが言えます。

- 変数が一度に持てる型は 1 つ
- 型によって変数の取れる値の範囲が異なる
- 変数同士のやり取りより関数とのやり取りの際に重要になる

#### 配列とは

**配列**とは、**一定の長さ**の、**連続した同じ型の値**を持つ変数です。  
次に `int` 型，長さ `3` の配列変数を定義する例を示します。

```c
int arr[3] = {1, 2, 3};
```

または、長さを明示せず、次のように書くこともできます。

```c
int arr[] = {1, 2, 3};
```

配列の長さを定義した後に変えることはできません。  
また、配列の長さを変数で設定することはできません。

```c
int x; scanf("%d", &x); // scanfは外部からの入力を受け取る関数
int a[x] = {1, 2, 3}; // コンパイルエラー！
```

配列の各要素の値を取得する方法に添え字を用いる方法があります。

```c
int arr[3] = {1, 2, 3};
arr[0]; // => 1
arr[1]; // => 2
arr[2]; // => 3
```

この際に注意すべきこととして、添え字の値は`(配列の長さ-1)`以下でなければなりません。これは配列の先頭の要素を `0` 番目としているからです。

#### 多次元配列

配列は、他の配列を要素に持つことができます。簡単な例を示します。

```c
int a[2][2] = { {1, 2}, {3, 4} };
```

上に示したのは 2\*2 の 2 次元配列です。
多次元配列においても基本的なルールは１次元の配列と変わりません。要素の値を取得する方法を次に示します。

```c
int a[2][2] = { {1, 2}, {3, 4} };
a[0][0]; // => 1
a[0][1]; // => 2
a[1][0]; // => 3
a[1][1]; // => 4

// つまり、a[0] = {1, 2}, a[1] = {3, 4}
```

なお、各次元の要素数を一致させる必要はなく、`int a[2][3]`なども問題ありません。

### C における関数

C において、**関数**は**複数の処理をまとめたもの**です。  
また、関数が持つ情報として、次のものがあります。

- 返り値の型
- 引数の型、個数
- (処理の内容)

関数の定義の構文を次に示します。

```c
返り値の型 関数名(引数1, 引数2, ...) {
	関数の内容
}
```

引数の数は特に制限されておらず、 `0` 個の場合もあります。
その場合でも、関数名の直後の括弧を省略することはできません。  
次に簡単な関数の定義の例を示します。 `2` 個の `int` 型の値を引数に取り、 `int` 型の値を返す `add` 関数を考えます。

```c
int add(int a, int b) {
	return a+b;
}
```

この関数をほかの関数から呼び出す例を次に示します。(今回は `main` 関数)

```c
int main() {
	add(2, 3); // 5
}
```

この関数の返り値を変数に代入して受け取ることもできます。

```c
int main() {
	int x = add(2, 3); // x = 5
}
```

代入先の変数の型と関数の返り値の型は一致している必要があります。

`add` 関数の引数に変数を渡す例を示します。

```c
int main() {
	int x = 12, y = 30;
	add(x, y); // 42
}
```

また、返り値のない関数を定義することもできます。

```c
void nothing() {
	puts("return nothing");
}
```

### C における条件分岐

C において、**条件分岐**は以下の 2 つがあります。

- `if` - `else` 文
- `switch` - `case` 文

#### `if` - `else` 文

`if` - `else` 文の構文を次に示します。

```c
if (条件1) {
	処理1
} else if (条件2) {
	処理2
} else {
	処理3
}
```

最初の `if` 文を省略することはできませんが、`else if` 、また `else` 節は必要に応じて省略することが可能です。省略した例を次に示します。

```c
// else 節のみ省略
if (条件1) {
	処理1
} else if (条件2) {
	処理2
}

// else if 節を省略
if (条件3) {
	処理3
} else {
	処理4
}

// 条件に当てはまらなかった時に特に何もする必要がない場合、 else 節、 else if 節をともに省略することができます
if (条件4) {
	処理5
}
```

#### `switch` - `case` 文

`switch` - `case` 文は `if` - `else` 文と機能的に似ているように見える文法ですが、いくつかの相違点があります。
例を示しながら、相違点を解説していきます。

```c
switch (式1) {
case 値1:
	処理1
	break;
case 値2:
	処理2
	break;
default:
	処理3
	break;
}
```

上の例を `if` - `else` 文で書くと次のようになります。

```c
if (式1 == 値1) {
	処理1
} else if (式2 == 値2) {
	処理2
} else {
	処理3
}
```

`if` - `else` 文と `switch` - `case` 文の相違点として、「`if` - `else` 文は条件(式)の真偽(値が 1 か 0 か)のみで分岐するのに対し、`switch` - `case` 文は 1 つの式に対してその値で分岐する」というものがあります。
(書いてから気づいたんですが、この文章は式とか文とか用語の説明をしなければいけないので、後に回したい。)  
また、`switch` - `case` 文では処理を書いたあとに(続けて次の条件の処理を必ず行いたいのでない限り)、 `break` 文を書かなければならないという点も異なります。
この文章では何が言いたいのか分かりにくいと思われるので、次にソースコードとその出力を示して説明します。

```c
#include <stdio.h>
int main() {
	int x = 4;

	switch (x) {
	case 2:
		puts("two!");
		break;
	case 4:
		puts("four!");
		// break を書き忘れてしまった!
	case 6:
		puts("six!");
		break;
	case 8:
		puts("eight!");
		break;
	default:
		puts("not supported!");
		break;
	}
}
```

さて、上に示したのは `int` 型の変数 `x` に対して分岐する単純なコードです。これをコンパイルして実行すると、

```
four!
six!
```

という出力が得られます。 `x` を他の数(`2`, `6`, `8`)に変更するとそれに対応した英単語単体が出力されると思います。  
ではなぜ `4` の時のみ `six!` という単語も出力されてしまうのかというと、`case 4:` に `break` 文を書き忘れてしまったためなのです。  
つまり、 `swtich` - `case` 文においては、各ケースに対して `break` 文を 1 つ書かないと自動的に次の `case` の処理に突入してしまうのです。
(ソースコードを見れば明らかかと思いますが、条件式の値が `case` の値と異なっていても突入してしまいます。)

### C におけるループ(繰り返し)処理

C において、ループ(繰り返し)処理は以下の 2 種類があります。

- `for` 文
- `while` 文(`do` \~ `while` 文)

#### `for` 文

`for` 文は次のような構文で表されるループ処理です。

```c
for (ループ用変数初期化式; ループ継続条件式; ループ用変数更新式) {
	処理
}
```

具体的な例として、1\~10 を数え上げるコードを紹介します。

```c
for (int i = 1; i <= 10; ++i) {
	printf("%d\n", i);
}
```

上記の構文と具体例を見比べてみます。  
`int i = 1` はループ用の変数 `i` の初期化式です。
ループ用変数とは、ループ継続条件式の真偽判定に使用する変数のことです。`for` 文以前で定義した変数を使用することもできます。  
`i <= 10` はループ継続条件式です。
この条件式を**満たさなくなったとき**にループは終了します。この条件式の判定は毎回のループの直前に行われます。
つまり初回ループ実行前にも行われるため、ループ内の処理が一度も行われないこともあり得ます。
ループ内の処理を必ず一度は行いたい場合、後述する [`do` \~ `while` 文](#do--while-文)を使用する必要があります。  
`++i` はループ用変数更新式です。**ループ用の変数を変化させるための式**をここに記述します。
ちなみにここに書かずにループの処理内に書くこともできますが、コードの可読性のためにこの部分に書くことをおすすめします。
(`for` 文でここ以外にループ用変数を変化させる式を書く人見たことない気がします。)

#### `while` 文(`do` \~ `while` 文)

`while` 文は次のような構文で表されるループ処理です。

```c
while (ループ継続条件式) {
	処理
}
```

具体例として、 `for` 文のセクションで紹介した、1\~10 を数え上げるコードを `while` 文で書いてみます。

```c
int i = 1;
while (i <= 10) {
	printf("%d\n", i);
	++i;
}
```

`for` 文との違いとして、ループ用変数の初期化を `while` より前に書いていること、ループ用変数更新式をループ処理内に書いていることが挙げられます。
これによって、`for` 文と異なり、**ループ用変数更新式を条件によって実行/スキップすることが容易**になっています。
(個人的には、情報が散逸して読みにくくなるため、更新式をスキップしたりするわけでなければ素直に `for` 文を使う方が好きです。)

#### `do` \~ `while` 文

`do` \~ `while` 文は、**ループの初回で条件チェックがない**ことを除けば、前述した `while` 文と機能は同じです。構文と具体例を示します。

```c
do {
	処理
} while (ループ継続条件式);
```

```c
int i = 5;
do {
	printf("%d\n", i);
	++i;
} while (i < 2);
// "5"のみ表示されてループ終了
// 通常の while 文では"5"すらも表示されない
```

## 実践編

### 文字の表示

例

```c
#include <stdio.h>
int main() {
	printf("Hello, MCC!\n");
	return 0;
}
```

実行すると `Hello, MCC!`という文字列が改行とともに表示されます。

#### 演習問題１

以下のテンプレートを用いて自分の Discord の名前を改行とともに表示してください。

テンプレート

```c
#include <stdio.h>
int main() {

	return 0;
}
```

<details>
<summary>演習問題１の模範解答</summary><div>

```c
#include <stdio.h>
int main() {
	printf("SSSato\n");
	return 0;
}
```

</div></details>

### 変数の内容の表示

変数の内容を `printf` 関数を用いて表示してみましょう。  
例

```c
#include <stdio.h>
int main() {
	int x = 42;
	printf("%d\n", x);
	return 0;
}
```

出力

```
42
```

`printf` 関数の引数に渡されている文字列に含まれている `%d` という文字列は「フォーマット指定子」と呼ばれ、`printf` 関数の第二引数以降に渡された値をどの型の値として解釈して表示するかを指定するものです。主要なフォーマット指定子には符号付き整数(`int`)の `%d` 、符号付き倍精度浮動小数点数(`double`)の `%lf` 、の符号付き文字(`char`)の `%c` 、`char`型ポインタ(文字列)の `%s` などがあります。(今覚える必要はないです。必要になった場面で毎回調べるたびに覚えるので。)

#### 演習問題２

次のテンプレートの `printf` 関数の第一引数内の"?"を適切なフォーマット指定子に変更して、`c` をそれぞれ整数(`int`)、文字(`char`)として解釈した結果を表示してください。  
テンプレート

```c
#include <stdio.h>
int main() {
	char c = 65;
	printf("%?, %?\n", c, c);
	return 0;
}
```

期待する出力

```
65, A
```

この出力から分かる通り、ASCII において、`'A'`の文字コードは`65`です

<details>
<summary>演習問題２の模範解答</summary><div>

```c
#include <stdio.h>
int main() {
	char c = 65;
	printf("%d, %c\n", c, c);
	return 0;
}
```

</div></details>  
  
　　

### 配列の内容の表示

配列変数の各要素を `printf` 関数を用いて表示してみましょう。  
例

```c
#include <stdio.h>
int main() {
	int arr[] = {12, 124, 1245};
	for (int i = 0; i < 3; ++i) {
		printf("%d\n", arr[i]);
	}
	return 0;
}
```

出力

```
12
124
1245
```

#### 演習問題３

多次元配列の各要素を表示してください。  
若干難易度が高いので、少し考えてコードが書けそうにない場合は模範解答を開いてしまってかまいません。  
テンプレート

```c
#include <stdio.h>
int main() {
	int arr[3][3] = {{12, 23, 34}, {54, 43, 32}, {46, 57, 68}};
	/* コードをここに書く */
	return 0;
}
```

<details>
<summary>演習問題３のヒント</summary><div>

二重ループを使います

</div></details>

<details>
<summary>演習問題３の模範解答</summary><div>

```c
#include <stdio.h>
int main() {
	int arr[3][3] = {{12, 23, 34}, {54, 43, 32}, {46, 57, 68}};
	for (int i = 0; i < 3; ++i) {
		for (int j = 0; j < 3; ++j) {
			printf("%d ", arr[i][j]);
		}
		printf("\n");
	}
	return 0;
}
```

出力

```
12 23 34
54 43 32
46 57 68
```

</div></details>

## 発展編

### 式、文について

式は値を返す。文は値を返さない。`1+1` は式。`if` 文や `switch` - `case`文は文だから値を返さない。`if` とか `switch` の括弧に入れられるやつは式。

### ポインタ(と配列)

書こうと思ったけど第二回に持ち越した方がよさそうな気がしたので持ち越します。
