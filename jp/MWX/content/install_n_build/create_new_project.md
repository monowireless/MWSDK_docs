---
title: "新しいプロジェクトの作成"
author: "Mono Wireless Inc."
description: "新しいプロジェクトの作成"
---

# 新しいプロジェクトの作成

新しいプロジェクトの作成は、すでにあるサンプルアクトのディレクトリを別の名前でコピーし、ファイル名の編集を行います。

{% hint style="warning" %}
コピー先のディレクトリは MWSDK 配下のディレクトリでなくても構いません。ただし、ディレクトリ名に**空白文字や日本語名が含まれてはいけません**。

MWSDK以外のディレクトリにコピーした場合 VS Code のワークスペース定義の一部が機能しなくなります。ワークスペースにmwxライブラリのソースコードディレクトリが追加されている場合は、新たに設定してください。

ライブラリソース設定をしなくても**ビルドには影響はありません**。より深いコード解釈をVSCode上で行い、編集効率を上げるための設定です。
{% endhint %}



プロジェクトのファイル構造は以下のようになっています（ここでは `PingPong `を例に挙げます）。

```
Act_samples
  +-PingPong
    +-PingPong.cpp   : アクトファイル
    +-build          : ビルドディレクトリ
    +-.vscode        : VS Code 用の設定ファイル    
```

この `PingPong `ディレクトリを別の場所（ただしディレクトリ名に日本語や空白が含まない）にコピーします。

```
SomeDir
  +-AlphaBravo
    +-PingPong.cpp -> AplhaBravo.cpp ※ファイル名を変更
    +-build          : ビルドディレクトリ
    +-.vscode        : VS Code 用の設定ファイル
```

編集の必要があるのは、`PingPong.cpp` のファイル名です。これをディレクトリ名と同じ`AlphaBravo.cpp`に変更します。

{% hint style="success" %}
`build\build-BLUE.cmd` を実行してBINファイルが生成されれば完了です（Windows10）。

Linux/WSL/macOS では`make TWELITE=BLUE`を実行して、ビルドが成功するか確認します。
{% endhint %}



{% hint style="info" %}
* ~~プロジェクトのディレクトリ名と同じ名前の .cpp ファイルは必須です。~~ (MWSDK 2020-04 では、任意のファイル名でOKになりました)
* ビルド対象のファイルを追加する場合は build/Makefile を編集します。編集方法は [Makefile の解説](makefile.md)をご覧ください。
{% endhint %}

