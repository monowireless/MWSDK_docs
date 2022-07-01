---
title: "アクトのビルド"
author: "Mono Wireless Inc."
description: "アクトのビルド"
---

# アクトのビルド

MWXライブラリで記述したアプリケーションプログラムをアクト(Act)と呼びます。まずは、これをビルドして書き込みます。

* ビルドディレクトリ構成について
* ビルドスクリプトについて
* VS Code でのビルドについて

{% hint style="info" %}
本ページでは、いくつかのビルド方法を記載していますが、いずれの方法も最終的にはmakeコマンドを実行しています。詳細は[Makefileの解説](makefile.md)を参照ください。
{% endhint %}



## ビルドディレクトリ構成について

MWSDKをインストールしたディレクトリ`MWSDK_ROOT (例 C:\MWSDK)`を開きます。以下のような構成になっています。

```
MWSDK_ROOT
  |
  +-ChipLib      : 半導体ライブラリ
  +-License      : ソフトウェア使用許諾契約書
  +-MkFiles      : makefile
  +-Tools        : コンパイラ等のツール一式
  +-TWENET       : TWENET/MWXライブラリ
  +-Act_samples  : アクトサンプル
  ...
```



アクトファイルは`Act_samples` 以下に格納しています。（以下は一部割愛しています）

```
Act_samples
  |
  +-CoreAppTwelite    : App_TweLiteと同じ構成のボード用のアクト
  +-PAL_AMB           : 環境センス PAL 用のアクト
  +-PAL_MAG           : 開閉センス PAL 用のアクト
  +-PAL_MOT           : 動作センス PAL 用のアクト
  ..
  +-Parent-MONOSTICK  : 親機アクト、MONOSTICK用
  +-PingPong          : PingPong アクト
  +-PulseCounter      : パルスカウンタを利用したアクト
  +-act0              : スクラッチ（とりあえず書いてみる）用アクト
```

これらのアクトは、MWXライブラリの記述の参考となるシンプルな例ですが、多くのアクトは以下の機能を有しています。

* センサー値を取得する
* センサー値取得後、無線パケットを親機宛に送信する
* 送信完了後、一定時間スリープする（または割り込みを待つ）

`Parent-MONOSTICK`のアクトによりパケットの受信と表示を行っています。この親機用のアクトは、アスキー形式で出力しています。 (`:00112233AABBCC...FF[CR][LF]` のような : で始まり、途中は１６進数のバイトをアスキー文字2字で表現する形式です。末尾の??は同様に2字のバイトとなりますがLRCというチェックサムバイトになります。参考：[アスキー形式](https://mono-wireless.com/jp/products/TWE-APPS/App\_Uart/mode\_format\_ascii.html))

実際に動作させてみるときは、以下の組み合わせを試してみてください。

| 親                                                        | 子                                                     | 解説                                                                  |
| -------------------------------------------------------- | ----------------------------------------------------- | ------------------------------------------------------------------- |
| [BRD\_APPTWELITE](../act\_samples/brd\_apptwelite.md)    | [BRD\_APPTWELITE](../act\_samples/brd\_apptwelite.md) | 親機はM1ピンをLOW(GNDレベル)にして起動する。通常モード（常時稼働）にて、App\_TweLiteのような動作を確認できます。 |
| [PingPong](../act\_samples/pingpong.md)                  | [PingPong](../act\_samples/pingpong.md)               | 子機同士2台使って動作します。片方から Ping パケットを送ると、相手方から Pong パケットが戻ってきます。           |
| [Parent-MONOSTICK](../act\_samples/parent\_monostick.md) | その他                                                   | 子機用のアクトのパケット送信を確認できます。                                              |



では、アクトの中から PingPong のディレクトリの中を見てみましょう。

{% hint style="info" %}
`Act_samples` にある他のアクトもビルドできます。その場合、ディレクトリ名・ファイル名は読み替えるようにしてください。
{% endhint %}

```
Act_samples
  +-PingPong
    +-PingPong.cpp   : アクトファイル
    +-build          : ビルドディレクトリ
    +-.vscode        : VS Code 用の設定ファイル
```

必ずディレクトリ直下にディレクトリと同名の `.cpp` ファイルが必要です。

{% hint style="info" %}
小規模なアクトならこの`.cpp`ファイル内に記述します。規模が大きくなってきたときは[Makefileの解説](makefile.md)を参考にして複数のファイルに分割してビルドすることが出来ます。
{% endhint %}

{% hint style="warning" %}
`PingPong` ディレクトリ直下にアクトファイル `PingPong.cpp` があります。ディレクトリ名を変更した場合は、必ず `.cpp` ファイルの名前もディレクトリ名と同名にします。
{% endhint %}



次にビルドディレクトリを開きます。

```
Act_samples
  +-PingPong
    +-build
      +-Makefile        : makefile
      +-build-BLUE.cmd  : TWELITE BLUE 用ビルドスクリプト
      +-build-RED.cmd   : TWELITE RED 用ビルドスクリプト
      +-build-clean.cmd : obj_* ファイル削除
```

ビルドに必要なスクリプトと`Makefile`が格納されています。



## ビルドスクリプト(Windows10)

{% hint style="warning" %}
macOS, Linux では[VS Code](building-act.md#vs-code-denobirudonitsuite)または[コマンドライン](building-act.md#komandorainlinuxmacoswskdenobirudo)によるビルドを行います。
{% endhint %}



ビルドスクリプトは、エラーがあまり出ることのない、完成済みのアクト、サンプル提供のアクトなどに向いています。

以下は **Windows10用のスクリプト（バッチファイル）**です。



| バッチファイル名       | 内容            |
| -------------- | ------------- |
| build-BLUE.cmd | TWELITE BLUE用 |
| build-RED.cmd  | TWELITE RED用  |

実行後にbinファイルが生成され`PingPong_BLUE_???.bin` または`PingPong_RED_???.bin` のファイル名になります。???はバージョン番号やライブラリのバージョン文字に置き換わります。

![PingPong アクトのディレクトリを開く](<../.gitbook/assets/image (23).png>)

![build-BLUE.cmd をダブルクリック(実行)](<../.gitbook/assets/image (24).png>)

![ビルド結果](<../.gitbook/assets/image (22).png>)

![BINファイル(PingPong\_BLUE\_L1203\_V0-1-0.bin) が出来ている](<../.gitbook/assets/image (25).png>)



{% hint style="success" %}
BINファイルが出来上がればビルド成功です。
{% endhint %}

{% hint style="info" %}
`objs_BLUE`ディレクトリはビルド中に生成された中間ファイルです。削除してもかまいません。
{% endhint %}

{% hint style="warning" %}
ビルドを迅速にするためパラレルビルドのオプションを設定しています。このためエラーが出た場合はエラーメッセージを視認しづらくなっています。

エラーメッセージを効率的に参照したい場合は VS Code などの開発ツールの利用を推奨します。
{% endhint %}



### クリーン（中間ファイルの削除）

`build-clean.cmd`を実行すれば、`objs_` で始まるディレクトリを消去します。BINファイルは消去しません。

{% hint style="warning" %}
ビルドがうまくいかない場合は、まずエラーメッセージを確認して下さい。errorという文字列が含まれる行中のメッセージから、エラー原因が容易に特定できる場合も少なくありません。

`objs_???` ディレクトリにある中間ファイルを削除してから再実行してみてください。（他の環境でビルドした中間ファイルが残っていると`make clean`を含めすべての操作が失敗します)
{% endhint %}



## コマンドライン(Linux/macOS)でのビルド

コマンドライン環境でのビルドについて補足します。

{% hint style="warning" %}
コマンドライン(bash)についての利用の知識が必要です。
{% endhint %}

{% hint style="danger" %}
OS環境によっては各実行プログラムの動作時にセキュリティ警告が出る場合があります。警告を抑制する設定が必要になります。（**警告を抑制してプログラムを動作する運用を行うか**は、お客自身またはシステム管理者に相談の上、ご判断ください）
{% endhint %}



コマンドラインでのビルドは、bash(Bourne-again shell)が動作するウインドウで`make`を実行します。事前に環境変数`MWSDK_ROOT`が正しく設定されていることを確認してください。例えば`C:/MWSDK`にインストールした場合は `~/.profile` に以下のような設定を行います。

```bash
MWSDK_ROOT=/mnt/c/MWSDK
export MWSDK_ROOT
```



コマンドライン(bash)よりmakeを実行します。`make`がない場合はパッケージをインストールする必要があります。

```bash
$ make

Command 'make' not found, but can be installed with:

sudo apt install make
sudo apt install make-guile

$ sudo apt install make
...
```

{% hint style="info" %}
* Linux/WSL環境では`make`または`build-essential`パッケージをインストールします。
* macOS環境ではXcodeでCommand Line Toolsをインストールします。
{% endhint %}



ビルドは以下のようになります。

```
$ cd $MWSDK_ROOT
$ cd Act_samples/PingPong/build
$ pwd
/mnt/c/MWSDK/Act_samples/PingPong/build

$ ls
... ファイル一覧の表示

$ rm -rfv objs_*
... 念のため中間ファイルを削除

$ make TWELITE=BLUE
... BLUE用に通常ビルド

$ make -j8 TWELITE=BLUE
... BLUE用にパラレルビルド(同時に8プロセス)
```



### 中間ファイルについて

ビルドが行われると objs\_??? ディレクトリが作成され、その中に中間ファイルが生成されます。このファイルはコンパイルした環境に依存しているため、他の環境のファイルが残っているとmakeがエラーとなりビルドが失敗します。

{% hint style="warning" %}
makeがエラーとなった場合は**直接`objs_???`ディレクトリ**を削除してください。
{% endhint %}



### コマンド例

詳細は[Makefileの解説](makefile.md)をご覧ください。

| コマンド例               | 解説                |
| ------------------- | ----------------- |
| `make TWELITE=BLUE` | TWELITE BLUE用にビルド |
| `make TWELITE=RED`  | TWELITE RED用にビルド  |
| `make cleanall`     | 中間ファイルの削除         |



## VS Code でのビルドについて

{% hint style="danger" %}
ビルドには TWELITE STAGE を推奨します。

MWSDK付属のサンプルプロジェクトのVS Code定義ファイルは可能な限り実施しますが、一部定義が不完全なものも含まれます。
{% endhint %}

{% hint style="danger" %}
OS環境によっては各実行プログラムの動作時にセキュリティ警告が出る場合があります。警告を抑制する設定が必要になります。（**警告を抑制してプログラムを動作する運用を行うか**は、お客自身またはシステム管理者に相談の上、ご判断ください）
{% endhint %}

VS Code では、Act\_samplesディレクトリ直下にあるワークスペースファイルを開くか、Act\_samples以下のアクトディレクトリを開きます。

{% hint style="warning" %}
以下の例では英語インタフェースの画面例で、ワークスペースを開いています。
{% endhint %}

ワークスペースを開き `[Terminal>Run Task...]` を選択します。

![ビルドタスクの一覧表示](<../.gitbook/assets/image (1).png>)



ビルドするTWELITE無線モジュールの種別(BLUE/RED)とアクト名を選択します。以下の例ではBuild for TWELITE BLUE PingPong (TWELITE BLUE用/PingPongアクト) を選択しています。選択後すぐにビルドが始まります。

![ビルドタスクの選択](<../.gitbook/assets/image (3).png>)



ビルド中の経過は画面下部の TERMINAL 部分に出力されます。

![ビルド経過](<../.gitbook/assets/image (20).png>)

{% hint style="success" %}
正しくビルドできた場合、上記画面例の反転表示部のように .elf ファイルが生成されるメッセージがサイズ情報(`text data bss dec hex filename`と記載がある部分)とともに出力されます。

またBINファイル（上記では `PingPong_BLUE_???.bin`）ファイルがbuildディレクトリ下に出来上がっているはずです。確認してみてください。
{% endhint %}

{% hint style="info" %}
ビルド定義には Windows10 のファイルシステムに適合しないディレクトリ名 (例：`/c/User/...`)を変換する(例：`C:/User/...`) 定義を追加しています。

変換は完全ではありませんが、コンパイルメッセージからエラーが発生しているファイル名と行番号を抽出できます。

`.vscode/tasks.json` 中の実行コマンドは `sh -c "make ... | sed -E -e s#..."` のようにコマンド呼び出しすることで、出力メッセージ中のドライブ名相当部の文字列を書き換えています。

```
...
"windows": {
    "command": "sh",
    "args": [
        "-c", "make TWELITE=BLUE 2>&1 | sed -E -e s#\\(/mnt\\)?/\\([a-zA-Z]\\)/#\\\\\\2:/#g"
    ],
```
{% endhint %}

{% hint style="warning" %}
ビルドがうまくいかない場合は、まず**エラーメッセージを確認**して下さい。**errorという文字列が含まれる行**中のメッセージから、エラー原因が容易に特定できる場合も少なくありません。

念のため、クリーン(`objs_???` ディレクトリにある中間ファイルの削除)を行い、ビルドを再実行してみてください。（他の環境でビルドした中間ファイルが残っていると`make clean`を含めすべての操作が失敗します)
{% endhint %}



## WSLについて

[WSL (Windows Subsystem for Linux)](https://docs.microsoft.com/en-us/windows/wsl/about) は Windows10 のサブシステムとして動作する Linux 環境です。

{% hint style="warning" %}
Windows10 では特別な理由がない限り**WSL (Windows Subsystem for Linux)は、MWSDKでアクトをビルドするのに必須ではありません**。WSLについて、既に知見があり特に利用したい方のみ本節をご覧ください。ここではWSLのインストール方法や使用方法については紹介しません。
{% endhint %}

### MWSDK2020\_05 .. 2020\_10

`MWSDK/Tools/ba-elf-ba2-r36379.w10` 以下に Windows10用とLinux用の実行形式が両方含まれます。WSLを動作させ環境変数MWSDK\_ROOTを適切に設定します。

例えば `C:\Work\MWSTAGE\MWSDK` の場合は以下のように設定します。

```
$ export MWSDK_ROOT=/mnt/c/Work/MWSTAGE/MWSDK
```

### MWSDK2020\_12

TWELITE STAGE SDK パッケージには、WSL用の実行形式は含まれません。

`MWSTAGE/Tools/ba-elf-ba2-r36379.wsl`というフォルダ名で、ツール一式を格納してください。ツールはMWSDK2020\_10の`MWSDK/Tools/ba-elf-ba2-r36379.w10`を用いるのが平易です。

### ツールの選択

`MWSDK/Tools/MkFiles/rules.mk`で環境の判定とツールディレクトリの選択をしています。以下は`rules.mk`の抜粋で`WSLENV`の環境変数の有無で判定しています。

```
# Configure for WSL (Windows Subsystem Linux)
ifneq ($(origin WSLENV),undefined)
$(info !!!WSL environment, use Linux toolchain instead.)
TOOLCHAIN_PATH = ba-elf-ba2-r36379.wsl
endif
```

