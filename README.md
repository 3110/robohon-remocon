# ロボホンリモコンアプリ

<a href="/images/robohon-remocon.png"><img src="/images/robohon-remocon.png" width=800></a>

ロボホンがスマートリモコンNature Remoと連携して家電を操作するロブリックアプリケーションです。ロボホンに話しかけることで，リモコンの赤外線信号の登録・削除・送信ができます。

## 必要なもの

* [ロボホン](https://robohon.com/)
* [ロブリック](https://robohon.com/apps/robrick.php)
* [Nature Remo Local API](https://local-swagger.nature.global/)に対応したNature Remoシリーズ  
  [Nature Remo 3](https://shop.nature.global/products/nature-remo-3)で動作確認をしていますが，[Nature Remo mini 2](https://shop.nature.global/products/nature-remo-mini-2)でも動くはずです。残念ながら[Nature Remo nano](https://shop.nature.global/products/nature-remo-nano_a)はLocal APIに対応していないので使えません。
* 無線WiFi環境  
  Nature Remoは2.4GHz帯のWiFi環境にしか接続できません。

## 事前準備

1. [Nature Remo セットアップマニュアル(初期設定方法)](https://support.nature.global/hc/ja/articles/900001792563)にそって初期設定を済ませてください。
2. [ロブリック](https://robohon.com/apps/robrick.php)のページの【インストール】に書かれている手順でインストールしてください。
3. 使用するNature RemoのIPアドレスを調べてメモしておいてください。Windows・Macの場合は，以下のようにNature RemoのMACアドレス（アプリや本体に書かれています）の下6桁を`Remo-`に続いて入力し，`.local`を付けて`dns-sd`コマンドに指定します。  
    ```bash
    $ dns-sd -G v4 Remo-XXXXXX.local
    Timestamp     A/R Flags if Hostname                  Address                                      TTL
    13:52:59.559  Add     2 20 Remo-XXXXXX.local.        192.168.11.109                               120
    ```
## インストール方法

1. `robohon-remocon.xml`をダウンロードします。
2. ロボホンでロブリックを起動し，表示されているIPアドレスとポート番号（18001）を指定してWebブラウザで開きます。  
3. 「読み込み」ボタンを押してダウンロードした`robohon-remocon.xml`を読み込みます。
4. 必要であれば待ち受け起動のキーワード「ネエロボホン」を変更します。
5. 変数「オーナー名」を変更します。
6. 変数「ローカルIPアドレス」をさきほどメモしたNature RemoのIPアドレスに変更します。  
   ※ロブリックのバグでこの設定が有効にならないため，バグが直るまでは関数「IR信号を送信する」・「IR信号を受信する」の中にあるWebAPIブロックのIPアドレスを直接変更してください。
7. 「保存」ボタンを押して，`robohon-remocon.xml`に上書き保存してください。
8. 「ロボホンに送信」ボタンを押して，ロボホンにプログラムをインストールします。

## 起動方法

ロボホンに向かって待ち受け起動に指定したキーワード（「ねえロボホン」）を話しかるとリモコンロボホンアプリが起動します。

起動後は音声入力待ちになり，「リモコンを覚えて」「リモコンを忘れて」「リモコンを教えて」「何ができる」の4つの音声コマンドを認識できます。

また，「リモコンを覚える」で覚えさせた音声コマンドを言うと，そのコマンドに対応したリモコンの赤外線信号をNature Remoから送信します。

## 「リモコンを覚える」コマンド

起動後に「リモコンを覚えて」というと，Nature Remoにリモコンの赤外線信号をロボホンに記録しておくことができます。ロボホンの指示に従って，記録したいリモコンボタンを操作してください。

リモコンを操作後，記録したリモコンの赤外線信号を送信するためのコマンドを聞かれますので，音声入力で指示してください。

例えば，ライトを消すリモコンボタンを操作して「ライトを消して」という音声コマンドとして記録した場合，起動後に「ライトを消して」と言うと，ライトを消すリモコンボタンの赤外線信号をNature Remoから送信できます。

## 「リモコンを忘れる」コマンド

起動後に「リモコンを忘れて」というと，ロボホンが覚えているリモコンの赤外線信号を消すことができます。「リモコンを覚えて」で覚えさせた音声コマンドを指定することで，その赤外線信号データを消すことができます。

## 「リモコンを教えて」コマンド

ロボホンが覚えている音声コマンドを教えてくれます。

## 「何ができる」コマンド

ロボホンリモコンアプリで何ができるか教えてくれます。合わせて，使用できる音声コマンドを教えてくれます。

--- 

## 参考

* [ロボホンリモコン（Nature Remoで家電と連携）](https://robotomo.robohon.com/announcements/z9hm2lg5zbejodqg)（[ロボホンともだち広場](https://robotomo.robohon.com/)）
* [ロブリック](https://robohon.com/apps/robrick.php)（[ロボホン公式ページ](https://robohon.com/)）
* [ロボホン用プログラミングツール ロブリック SR-SA04 利用マニュアル Version 1.4.0](https://robohon.com/apps/robrick/robrick-manual_v1-4-0.pdf)
* [Nature Remo](https://nature.global/)
