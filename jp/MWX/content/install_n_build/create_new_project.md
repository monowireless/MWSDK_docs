---
title: "新しいプロジェクトの作成"
author: "Mono Wireless Inc."
description: "新しいプロジェクトの作成"
---

# 新しいプロジェクトの作成

新しいプロジェクトの作成は、すでにあるサンプルアクトのフォルダを別の名前でコピーし、ファイル名の編集を行います。

{% hint style="warning" %}
コピー先のフォルダは MWSDK 配下のフォルダでなくても構いません。ただし、フォルダ名に**空白文字や日本語名が含まれてはいけません**。

MWSDK以外のフォルダにコピーした場合 VS Code のワークスペース定義の一部が機能しなくなります。ワークスペースにmwxライブラリのソースコードフォルダが追加されている場合は、新たに設定してください。

ライブラリソース設定をしなくても**ビルドには影響はありません**。より深いコード解釈をVSCode上で行い、編集効率を上げるための設定です。
{% endhint %}



プロジェクトのファイル構造は以下のようになっています（ここでは `PingPong `を例に挙げます）。

```
Act_samples
  +-PingPong
    +-PingPong.cpp   : アクトファイル
    +-build          : ビルドフォルダ
    +-.vscode        : VS Code 用の設定ファイル    
```

この `PingPong `フォルダを別の場所（ただしフォルダ名に日本語や空白が含まない）にコピーします。

```
SomeDir
  +-AlphaBravo
    +-PingPong.cpp -> AplhaBravo.cpp ※ファイル名を変更
    +-build          : ビルドフォルダ
    +-.vscode        : VS Code 用の設定ファイル
```

編集の必要があるのは、`PingPong.cpp` のファイル名です。これをフォルダ名と同じ`AlphaBravo.cpp`に変更します。

{% hint style="success" %}
`build\build-BLUE.cmd` を実行してBINファイルが生成されれば完了です（Windows10）。

Linux/WSL/macOS では`make TWELITE=BLUE`を実行して、ビルドが成功するか確認します。
{% endhint %}



{% hint style="info" %}
* ~~プロジェクトのフォルダ名と同じ名前の .cpp ファイルは必須です。~~ (MWSDK 2020-04 では、任意のファイル名でOKになりました)
* ビルド対象のファイルを追加する場合は build/Makefile を編集します。編集方法は [Makefile の解説](makefile.md)をご覧ください。
{% endhint %}

