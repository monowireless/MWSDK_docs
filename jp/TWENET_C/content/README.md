# TWELITE SDK (MWSDK) マニュアル

| [English Document](https://sdk.twelite.info/v/en/) |
| -------------------------------------------------: |



TWELITE SDK は、モノワイヤレス株式会社が製造販売する TWELITE (トワイライト) 無線モジュールのファームウェアをビルドするための環境を提供します。本資料では MWSDK と記述することもあります。

{% hint style="info" %}
TWELITE によるアプリケーションの書き換えやプログラミングを行う場合は、まず以下を参照ください。
{% endhint %}

|               | 詳細                                                                                                                                    |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| TWELITE STAGE | ビルド、書き込み、ビューア（ターミナルや簡易モニタなど）を、一つのアプリで行えます。→ <a href="https://mono-wireless.com/jp/products/stage/">TWELITE STAGEの解説</a> |
| MWXライブラリ      | `setup(), loop()` を定義するより単純なプログラミングを行うためのC++ライブラリです。→ <a href="https://mwx.twelite.info">MWXライブラリの解説</a>     |



TWELITE SDK (MWSDK) には以下が含まれます。

* コンパイルを行うためのツール群 (gcc, make など)
* TWELITE NET ライブラリ
  * マイコンなどの低水準ライブラリを含む
  * mwx ライブラリ
  * その他、ライブラリ
* TWELITE SDK マニュアル（本資料）
  * MWSDK ディレクトリや MWSDK全般の解説。
  * TWELITE STAGEを用いずに、アプリを書き換えたり、ソースコードからビルドする方法。
  * ファームウェア書き換え方法についての詳細。
  * 無線パケットや中継ネットワークについての解説。
  * TWELITE NET C ライブラリの API についての解説 
    * イベントループなど内部処理の解説。



### 本資料の記載内容について

下記に関する用語については、文中では特に説明を行っていません。

* C言語によるマイコン開発について
* bash, make などコマンドラインの利用
* gcc ツールチェインの利用



### 本資料の表記について

* ディレクトリ（パス）区切りを / (スラッシュ) で統一します。Windows では \ (バックスラッシュまたは円マーク) ですが、読み替えて下さい。
* 表中で `\ ` ( バックスラッシュと空白) の２文字を挿入している場合があります。表示時に途中改行を促すものです。(例: `veryVeryLong\ DefName` は `veryVeryLongDefName`  と読み替えてください。
