
## 実デバイスへのデプロイ（Pixelbook）

自己責任でお願いします。

### PixelbookでFuchsiaを動作させた例

サムネイルをクリックするとYoutubeへ
[![](https://img.youtube.com/vi/sPDJZDC82n0/0.jpg)](https://www.youtube.com/watch?v=sPDJZDC82n0)

### 必要なもの

- Pixcelbook
- FuchsiaをビルドしたPC（以降、 **ホストPC** と呼ぶ）
- USB-C -> Ethernetアダプタ
  - まだWiFiが使えないために有線化が必要。ChromeOSの状態で認識できていたアダプタもFuchsiaでは認識しないことがあり、やや厳しい。Type-A -> Type-C -> Ethernetの変換だと私はうまくいかなかった。HUB経由ではなく直差しが必須と思われる。
- USBメモリ（USB-C）
  - 比較的どのようなものでもいける印象。私はHUB経由でも問題なかった。

### 前提・準備

- ホストPCで、x64ターゲットのTopazのビルドが完了していること TODO:ビルド
- zedbootが書き込まれたUSBメモリを作成済みであること TODO:zedboot
- ホストPCとPixelbookが通信可能な同一のネットワーク上にあること
- PixelbookのChromeOSのバージョンが62以上であること
- Pixelbookの全てのデータが消えてしまうので、必要なバックアップを取っていること

### Developer Modeへの切り替え

1. Pixelbookの電源を落とす
1. `Esc`キーと`Refresh`キー（キーボード最上部の一番左のキーと左から三番目のキー）の双方を押しっぱなしで、`Power`ボタンを押すと`Recovery Mode`で起動する
1. この画面で`Ctrl+D`を押すと`Developer Mode`に切り替えることができる
1. デバイスが再構成されるのでしばらく待つ
1. やがて大きなビープ音が2度鳴る


### USBから起動する準備

1. ChromeOSを起動
1. **OS verification is OFF** という画面が表示されるのでそのまま待つ。30秒ほど経過すると、ようこそ画面が出る
1. `Ctrl+Alt+Refresh` を押したまま`F3`キーを押してシェルを開く
1. ユーザー `chronos`、パスワードなしでログインする
1.  `sudo crossystem dev_boot_usb=1` でUSB起動を有効にする
※この状態のまましばらく放置してホストPCの準備へ移る

### ホストPCの準備

ホストPCのシェルで `fx boot vboot` を実行。以下のように待受状態になる。

```
$ fx boot vboot
2018-05-11 20:24:56 [bootserver] listening on [::]33331
```

### USBからの起動

1. zedbootが書き込まれたUSBメモリをPixcelbookに接続する
1. `sudo reboot` などでChromeOSを再起動する
1. **OS verification is OFF** という画面が表示されるので、`Ctrl+U` を押す。
1. そうするとUSBからzedbootが起動してPaveされる（ホストPCからFuchsiaのイメージを取得する）。以下のような画面が表示されていればok。うまくいけば、やがてFuchsiaが起動する。

![img_20180511_132616](https://user-images.githubusercontent.com/950356/40243519-643f9202-5afb-11e8-8d8f-c517c8528745.jpg)

### 何かのはずみでPixelbookが起動しなくなった場合のリスタート方法

1. `Refresh`キー（キーボード最上部の左から三番目のキー） + `Power`ボタンを長押しする
2. 10秒程度経過したらボタンとキーから指を放すと起動する
3. 起動しない場合は、再度`Power`ボタンを押す

### ChromeOSに戻す方法

TODO
