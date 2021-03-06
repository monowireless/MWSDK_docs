# 無線パケット

## 宛先について

無線パケットを配送する際には宛先情報が必要になります。宛先は３つの要素を意識する必要があります。

* チャネル
* アプリケーションID
* 宛先アドレス

チャネルは物理的な通信チャネルのことで ch11 〜 26 までの合計１６チャネルが指定できます。通信チャネルが違う場合は、物理的に受信することができません。通信をするにはまず、通信チャネルを一致させる必要があります。

通信チャネルが同じであっても、複数の無線システムを稼働できる必要があります。TWENET を用いるシステムが同じ場所に複数あって同じチャネルで通信する可能性がある場合は、アプリケーションIDにより別々のネットワークとして取り扱います。

最後に、チャネルもアプリケーションIDも一致していれば、宛先アドレスを適切に設定すれば通信が可能となります。宛先アドレスは、ショートアドレス（12bit 値の範囲で任意に設定できる）、ロングアドレス（個体識別アドレスで通信する）、同報通信の３種類があります。

## 送り主のアドレス

TWELITE NET では、送り主のアドレスをショートアドレスまたはロングアドレスとして送信できます。

## パケットの最大長

無線パケットは IEEE802.15.4 規格のパケット構造を元になっていますが、宛先データやTWENET で用いるヘッダなどユーザが直接利用しないデータを差し引いた分が最大で通信できるデータサイズとなります。

データサイズを小さくする（ペイロードを節約する、ショートアドレスを積極的に利用する）ことで電流消費の多い無線通信時間を短縮できます。また小さいパケットは比較的失敗しにくくなります。

