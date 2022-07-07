---
title: "アクトの実行"
author: "Mono Wireless Inc."
description: "アクトの実行"
---

# アクトの実行

ここではアクト(BINファイル)の書き込みと実行について解説します。

{% hint style="warning" %}
この節はWindows10環境のユーティリティTWE-Programmerを用いた解説です。

Linux/macOSでは[tweterm.py](tweterm.py.md)を用います。**本ページでの書き込み・実行の流れを参照いただいた上**、tweterm.pyを利用ください。
{% endhint %}



{% hint style="info" %}
TWE-Programmer, tweterm.pyはBINファイルの書き込み機能とターミナル機能がありますが、ターミナル機能については各システム用のターミナルソフトを利用することもできます。

* Windows10: TeraTerm
* Linux/macOS: screen など
{% endhint %}



## BINファイルの書き込みと実行

出来上がったBINファイルをTWELITEに書き込むにはTWE-Programmerを使用します。詳しい使い方は[こちら](https://tweprogrammer.twelite.info)を参照ください。

{% hint style="danger" %}
BINファイルが出来上がれば、実機で動作させることになります。繊細な電子部品ですので、取り扱いには十分注意してください。以下に代表的な注意事項を記載します。

特にTWELITE Rを用いている場合は、多くの場合電子基板がケースなどを介さず直接外部に触れる状態で使用するため、意図しないショートやノイズなどUSBデバイスが正常に動作しない状態になる場合があります。

この場合は、アプリケーションを終了させUSBデバイスを抜き差しすることで通常は回復します。最悪、USBデバイスの破損やPCの破損も考えられます。

電子基板の取り扱いには十分注意してください。

* 回路の間違い
  * 電源を入れる前には**もう一度**回路を確認してください。
  * 電池の**逆差しや過大電圧**には注意してください。
* 静電気
  * 人感がない電圧であっても半導体の故障になりえます。大掛かりな対応をしなくとも、金属部に触れてから作業する・リストバンド・専用マットなど簡易にできる対応でも相応の効果はあります。
* 金属物などが触れることでのショート
  * 電子基板の近くには金属物がないようにしてください。クリップなどが散らかっているとこれが原因でショートすることもありますし、電池が大放電して加熱する危険な状況も考えられます。
{% endhint %}



### 1. 事前に MONOSTICK や TWELITE R をPCに差し込んでドライバのセットアップを終了しておく。

デバイスが認識されれば、新たにCOMポートが追加されます。複数あってわかりにくい場合は、抜いた状態でのCOMポートと刺した状態でのCOMポートの様子を観察してみてください。

![デバイスマネージャーの画面例](<../../.gitbook/assets/image (10).png>)

{% hint style="warning" %}
デバイスマネージャでデバイスの存在が確認できない場合は、[FTDI社のドライバ](https://www.ftdichip.com/Drivers/VCP.htm)導入を行ってみてください。FT232R用のドライバを選択します。
{% endhint %}

### 2. TWE-Programmer.exe を起動する。

{MWSDKインストールフォルダ}/Tools/TWE-Programmerフォルダを開き、TWE-Programmer.exe をダブルクリックします。

![](<../../.gitbook/assets/image (9).png>)

TWE-Programmer.exe を起動すると以下のような画面になります。画面例では、起動前に MONOSTICK を差し込んでいて COM6 に割り当てられています。

![](<../../.gitbook/assets/image (11).png>)

{% hint style="warning" %}
MONOSTICK や TWELITE R が表示されない場合は以下を試してください。

* TWE-Programmer を終了する。
* MONOSTICK や TWELITE RをPCから抜く（取り外す）。
* もう一度MONOSTICK や TWELITE Rを差し込む。
* TWE-Programmer を起動する。

これでもうまくいかない場合は以下も試してください。

* PCから可能な限り他のUSBデバイスを取り外す。
* PCを再起動してからMONOSTICK や TWELITE Rを差し込んでみる。
* FTDI社のドライバを再導入してみる。
{% endhint %}



### 3. TWE-Programmer 上で BIN ファイルを指定する。

![](<../../.gitbook/assets/image (12).png>)



ファイルダイアログから BIN ファイルを指定します。

![BINファイルの選択](<../../.gitbook/assets/image (26).png>)

### 4. BINファイルの書き込み

BINファイルの書き込みは、BINファイルを指定すると自動で行われます。

![BINファイル書き込み中](<../../.gitbook/assets/image (15).png>)



### 5-1. 書き込み成功時

{% hint style="success" %}
書き込みが成功するとTWELITEは自動でリセットして、ターミナルが表示されます（ターミナル接続するにチェックが入っている場合）。

MWSDK添付のアクトファイルは始動時にメッセージを表示します。何か表示されれば書き込みは無事終了し、TWELITE 無線モジュール上のアクトが無事に動作していることが確認できます。
{% endhint %}

![書き込み後（ターミナルが起動し始動メッセージが表示）](<../../.gitbook/assets/image (16).png>)

{% hint style="info" %}
ターミナルを開いたままで、アクトを編集して再度書き込みたいときは`Ctrl+Alt+W`キーを押します。
{% endhint %}



### 5-2. 書き込み失敗時

書き込みに失敗したときは、ターミナルは開かず、TWE-Programmerのウインドウ背景がピンク色になります。

![書き込み失敗時の画面例](<../../.gitbook/assets/image (18).png>)

{% hint style="warning" %}
書き込みが失敗したときは (再)書き込みボタンを押して、もう一度書き込みを実行してください。

TWE-Programmer が反応しないなど、うまくいかない場合は、以下を実行した上、USBへの接続からやり直してください。

* TWE-Programmer を終了する
* MONOSTICK や TWELITE Rを取り外す

場合によってはPCの再起動を行ってください。
{% endhint %}

{% hint style="warning" %}
TWELITE PAL での書き込み中に、ハードウェア・ウォッチドッグタイマーが作動し書き込みが中断する場合があります。再度、書き込みを行ってください。
{% endhint %}
