---
title: サンプルアクト
author: "Mono Wireless Inc."
description: Sample Acts
---

# サンプルアクト

アクトの動作を理解するため、いくつかのサンプルを用意しています。

{% hint style="info" %}
**サンプルは MWSDK をインストールしたディレクトリにある `Act_samples `にあります。**
{% endhint %}

## サンプルアクトの紹介

以下は上から順に見ていただく

[act0..4](act\_opening.md)は、無線機能などを使わないごくシンプルな例です。Actの基本構造が理解できます。

[Scratch](scratch.md) は、UARTから１バイトコマンドを受けて、送信などを行うシンプルなコードです。

[Slp\_Wk\_and\_Tx](slp\_wk\_and\_tx.md)は、ステートマシンを用い、スリープを用いた間欠動作で、スリープ復帰→無線送信→スリープを繰り返します。

[Parent\_MONOSTICK](parent\_monostick.md)は、専ら受信のみを行い、シリアルポートへ受信結果を出力します。このサンプルの無線パケットで、親機向け(0x00)や子機ブロードキャスト(0xFE)とアドレス設定しているものは受信できます。またインタラクティブモード[\<STG\_STD>](../settings/stg\_std.md)をActに追加するための手続きが含まれます。

[PingPong](pingpong.md)は、一方から他方にパケットを送信し、受信した他方がパケットを送り返すサンプルです。送信と受信についての基本的な手続きが含まれます。

[BRD\_APPTWELITE](brd\_apptwelite.md)はディジタル入力、アナログ入力、ディジタル出力、アナログ出力を用いた双方向通信を行っています。またインタラクティブモード[\<STG\_STD>](../settings/stg\_std.md)をActに追加するための手続きが含まれます。

[PAL\_AMB](pal\_amb.md), [PAL\_MOT-single](pal\_mot-oneshot.md), [PAL\_MAG](pal\_mag.md)は、各種PAL基板用のサンプルです(TWELITE CUEでもサンプルの定義を変更することでPAL\_MOT,PAL\_MAGを実行できます)。PAL基板上のセンサー値を取得し、送信し、スリープします。

### 応用編のアクト

* [PAL\_AMB\_usenap](pal\_amb-usenap.md) は、数十msかかるセンサーの動作時間にTWELITEマイコンを短くスリープさせ、より省電力を目指すサンプルです。
* [PAL\_AMB\_behavior](pal\_amb-behavior.md) は、ビヘイビアを用いた例です。PAL\_AMBでは温湿度センサーはライブラリ内部のコードが呼ばれますが、このサンプルでは温湿度センサーのアクセスのための独自の手続きも含まれます。
* [PAL\_MOT\_fifo](pal\_mot.md) は、加速度センサーのFIFOおよびFIFOの割り込みを用いて、サンプルを中断することなく、連続的に取得し無線送信するためのサンプルです。
* [PulseCounter](pulsecounter.md) は、パルスカウンター機能を用い、スリープ中も含め入力ポートで検出したパルス数を計数し、これを無線送信します。
* [WirelessUART](wirelessuart.md)は、UART入力を[serparser](../api-reference/classes/ser\_parser.md)を用いアスキー形式を解釈し、これを送信します。
* Setting は、インタラクティブモード[\<STG\_STD>](../settings/stg\_std.md)のより高度なカスタマイズを行います。



### 単体機能を紹介したAct

[Unitから始まる名前のAct](unit\_acts.md)は機能やAPIの紹介を目的としています。



## 最新版の入手

{% hint style="info" %}
最新版のコードや MWSDK バージョン間の修正履歴を確認する目的で Github にソース一式を置いています。以下のリンク先を参照してください。

[https://github.com/monowireless/Act\_samples](https://github.com/monowireless/Act\_samples)
{% endhint %}



## 共通の記述

アクトのサンプル中で以下の項目は共通の設定項目になり、以下で解説します。

```cpp
const uint32_t APP_ID = 0x1234abcd;
const uint8_t CHANNEL = 13;
const char APP_FOURCHAR[] = "BAT1";
```

{% hint style="info" %}
サンプルアクト共通として以下の設定をしています。

* アプリケーションID ` 0x1234abcd`
* チャネル `13`

アプリケーションIDとチャネルはともに他のネットワークと混在しないようにする仕組みです。

**アプリケーションIDが異なる者同士は、チャネルが同じであっても混信することはありません**。ただし、別のアプリケーションIDのシステムが頻繁に無線送信しているような場合はその無線送信が妨害となりますので影響は出ます。

チャネルは通信に使う周波数を決めます。TWELITE無線モジュールでは原則として**１６個のチャネル**が利用でき、通常のシステムでは実施しないような極めて例外的な場合を除き、**違うチャネルとは通信できません**。

サンプルアクト共通の仕様として、パケットのペイロード(データ部)の先頭には4バイトの文字列(`APP_FOURCHAR[]`)を格納しています。種別の識別性には1バイトで十分ですが、解説のための記述です。こういった**システム特有の識別子やデータ構造**を含めるのも混信対策の一つです。
{% endhint %}

