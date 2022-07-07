---
title: "TWELITE SDK のインストール"
author: "Mono Wireless Inc."
description: "TWELITE SDK のインストール"
---

# TWELITE STAGE SDK のインストール
{% hint style="info" %}
TWELITE STAGE SDK をダウンロードした場合は、配布アーカイブ(ZIPなど)を、**日本語や空白文字が含まれない**フォルダに展開します。

TWELITE STAGE については以下もご覧ください。

* [概要・ダウンロード](https://mono-wireless.com/jp/products/stage)
* [マニュアル](https://stage.twelite.info)

{% endhint %}


### 3. 環境変数の設定

{% hint style="warning" %}
TWELITE STAGE アプリを用いる場合は、**環境変数の設定は不要**です。コマンドラインでビルドを行う場合は設定してください。
{% endhint %}



`MWSDK_ROOT`, `MWSDK_ROOT_WINNAME`(Windows10のみ) の設定が必要です。

#### Windows
ここでは展開後のフォルダ名を `C:\MWSTAGE `とします。別のフォルダにインストールした場合は、読み替えてください。

`C:\MWSTAGE\Tools\SET_ENV.CMD` を実行してください。以下の環境変数を設定します。

* `MWSDK_ROOT`
* `MWSDK_ROOT_WINNAME`

例えば以下のような設定になります。

```
MWSDK_ROOT=C:/MWSTAGE/MWSDK/
MW_ROOT_WINNAME=C:\MWSTAGE\MWSDK\
```



{% hint style="warning" %}
インストールしたPC上からTWELITE STAGE SDKをアンインストールするには以下を行ってください。

* `UNSET_ENV.cmd`を実行してください。環境変数の設定を解除します。
* MWSTAGEフォルダを削除してください。
{% endhint %}

#### Linux
開発環境やシェルに `MWX_ROOT`環境変数を反映されるように設定してください。

方法はいくつかありますが、ホームフォルダの`.profile`（ファイルがなければ新しく作成してください）に以下の設定を追加します。この設定でVSCodeのビルドまで可能です。

`MWSDK_ROOT=/foo/bar/MWSTAGE/MWSDK/`\
`export MWSDK_ROOT`



エディタを使用せずに追加するには以下のようにコマンド入力します。`$`はプロンプトで環境によって表示が違います。`/foo/bar/MSWSDK`の部分はインストールしたフォルダに応じて書き換えてください。

```bash
$ cd $HOME
$ echo MWSDK_ROOT=/foo/bar/MWSTAGE/MWSDK>>.profile
$ echo export MWSDK_ROOT>>.profile
```

#### macOS
開発環境やシェルに `MWX_ROOT`環境変数を反映されるように設定してください。



方法はいくつかありますが、ホームフォルダの`.profile`（ファイルがなければ新しく作成してください）に以下の設定を追加します。この設定でVSCodeのビルドまで可能です。

`MWSDK_ROOT=/foo/bar/MWSTAGE/MWSDK/`\
`export MWSDK_ROOT`



エディタを使用せずに追加するには以下のようにコマンド入力します。`$`はプロンプトで環境によって表示が違います。`/foo/bar/MSWSDK`の部分はインストールしたフォルダに応じて書き換えてください。

```bash
$ cd $HOME
$ echo MWSDK_ROOT=/foo/bar/MWSTAGE/MWSDK>>.profile
$ echo export MWSDK_ROOT>>.profile
```



{% hint style="info" %}
環境全体に`MWSDK_ROOT`を適用にするにはLaunchDを用います。

VS Codeの一部の設定で環境変数を参照していますが、ビルドには必須ではありません。
{% endhint %}



### 4. ライブラリの修正の適用

SDKに収録された時点から、ライブラリソースコードに修正がある場合があります。[改版履歴](../revisions.md)を参照の上、必要に応じでライブラリソースコードを差し替えてください。



