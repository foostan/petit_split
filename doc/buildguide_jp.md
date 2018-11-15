# Build Guide

## 部品
| 名前 | 数 | 備考 | 
|:-|:-|:-|
| PCB | 2枚 | 面付されています |
| トッププレート | 2枚 | |
| ボトムプレート | 2枚 | |
| ProMicro | 2枚 | |
| TRRSジャック | 2個 | |
| タクトスイッチ | 2個 | |
| ダイオード | 8個 | チップ部品のみに対応 |
| Kailh PCBソケット CherryMX用 | 8個 | |
| Kailh PCBソケット Choc用 | 8個 | |
| キースイッチ(CherryMX用 or Choc用) | 8個 | |
| キーキャップ(CherryMX用 or Choc用) | 8個 | |
| スペーサー M2 6.5mm | 8本 | |
| ネジ M2 4mm | 16本 | |
| クッションゴム | 8個 | |
| TRS(3極)ケーブル | 1本 | TRRS(4極)ケーブルでも可 |
| Micro USBケーブル | 1本 | |

![image](https://user-images.githubusercontent.com/736191/48524659-95d81300-e8c4-11e8-9c26-033c90b91878.png)

## 実装

面付を切り離し、どちらを左手(右手)にするか決めておきます。

![image](https://user-images.githubusercontent.com/736191/48524696-b7d19580-e8c4-11e8-810c-2eaae36cae89.png)

### リセットスイッチとTRRSジャックの取り付け

まずはリセットスイッチとTRRSジャックを付けていきます。
写真の位置にはんだ付けします。

![image](https://user-images.githubusercontent.com/736191/48524753-ec455180-e8c4-11e8-8855-08e2a0d7e856.png)

### ProMicroの取り付け

次にProMicroを取り付けていきます。

ProMicroの裏側が正面に来るようにピンヘッダを取り付けます。
またこのピンヘッダがシルクの白い枠に収まるようにPCBに取り付けます。

このキーボードに限らずProMicroについてはシルクでピンの情報が書かれています(RAWやGNDなど)。
もし取り付け位置がわからない場合は、ProMicro側のシルクとPCB側のシルクが合うようにすると間違いが防げます。

![image](https://user-images.githubusercontent.com/736191/48524845-46461700-e8c5-11e8-8c19-07bafc990e12.png)

### ダイオードの取り付け

次にダイオードを取り付けていきます。

量が少ないので両手分いっきに取り付けます。
片側を反転させて、取り付けるダイオードの向きを両手分で揃えておくと間違いなくスムーズに取り付けられます。

![image](https://user-images.githubusercontent.com/736191/48524891-68d83000-e8c5-11e8-87b2-4d8e36540ab2.png)

### PCBソケットの取り付け

次にPCBソケットを取り付けていきます。
なおはんだ付けはこれで最後です。

PCBソケットのパッド部分はギリギリの大きさになっているので、先にはんだを両足分盛っておきます。
予備ハンダのイメージですが後からはんだを追加し難いので多少多めに盛っておきます。

あとはソケットを穴にはめて指で抑えながら、盛ったはんだを溶かして接着します。

![image](https://user-images.githubusercontent.com/736191/48524959-a3da6380-e8c5-11e8-8e39-68f60013d2bf.png)

### プレートの取り付け

最後にプレートを取り付けていきます。

プレートにスペーサーを取り付け、キースイッチをトッププレートにはめます(後からでもいいですが先のほうが楽)。
あとはここにかぶせるようにPCBをはめます。キースイッチが全てPCBソケットにはまっていることが確認できればOKです。

最後にボトムプレートを取り付け、ゴム足を貼れば完成です。

![image](https://user-images.githubusercontent.com/736191/48525051-fae03880-e8c5-11e8-8d8d-305140bd3608.png)

## ファームウェア
https://docs.qmk.fm/#/newbs_getting_started こちらを参照して頂き、ファームウェアを書き込む環境を用意します。
Petit Splitのファームは本家にマージされていないので、`https://github.com/foostan/qmk_firmware/tree/petit_split` をクローンして使ってください。

環境ができましたら、下記コマンドで Petit Split 用にファームウェアをビルドします。

```
make petit_split:default
```

ビルドが完了したら下記コマンドを実行します。

```
make petit_split:default:avrdude
```

実行すると下記のようなログがでて、`.` が増えていくことが確認出来ると思います。
この間にリセットスイッチを __2回__ 押すとファームウェアの書き込みが完了します。

```
<省略>

Checking file size of petit_split_rev1_default.hex                                                        [OK]
 * File size is fine - 27328/28672
Copying crkbd_rev1_default.hex to qmk_firmware folder                                               [OK]
Detecting USB port, reset your controller now........
```

片側のProMicroにファームウェアの書き込みが完了したら、もう片方も同じ手順で書き込みを行います。

以上で完成です。

