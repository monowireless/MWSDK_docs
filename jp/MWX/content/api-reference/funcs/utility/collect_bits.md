---
title: "collect_bits()"
author: "Mono Wireless Inc."
description: "collect_bits()"
---
# collect\_bits()

整数から指定したビット位置の値を取得し、指定した順番のビットマップを作成します。

```cpp
constexpr uint32_t collect_bits(uint32_t bm, ...)
```

  パラメータbmに指定する値から、その後の可変数パラメータで指定する0..31のビット位置に対応する値を取り出します。取り出した値はパラメータ順に並べビットマップとして戻り値になります。

ビットマップの並び順は、最初のパラメータを上位ビットとし末尾のパラメータがbit0になります。

```cpp
uint32_t b1 = 0x12; // (b00010010)
uint32_t b2 = collect_bits(b1, 4, 2, 1, 0); 
  // bit4->1, bit2->0, bit1->1, bit0->0
  // b2=0x10 (b1010)
```

例ではb1のビット4,2,1,0を取り出すと (1,0,1,0) になります。これをb1010として0x10のように計算されます。&#x20;

## 背景

IOポート(DI,DO)の状態など各種ビットマップに値を参照・設定する場面があり、その記述を簡素化するため。
