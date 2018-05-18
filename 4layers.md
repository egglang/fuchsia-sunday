## 4つのレイヤー

Fuchsiaは大きく4つのレイヤーで構成されており、これらのレイヤーを重ねた状態をケーキ(layer cake)に喩えている。

![レイヤー](https://user-images.githubusercontent.com/950356/40233022-33921342-5adc-11e8-87e1-91e76f8a85f3.jpg)

### Zircon（旧称:Magenta）

[Zircon](https://fuchsia.googlesource.com/zircon) はいわゆるカーネル部分。Linuxではなく、LK (Little Kernel) をベースとしている。LKはAndroidのブートローダーや[Trusty TEE](https://source.android.com/security/trusty/) にも実際に利用されている。
AndroidやChrome OSなどのOSはLinux上に構築されるが、FuchsiaはZircon上に構築される。つまりFuchsiaはLinuxではなく、システムコールもLinuxのそれとは異なっている。
加えて、Zirconはシステム内のプロセス間通信で利用されるFuchsia IDL（FIDL）と、C/C++のバックエンドを提供する。


### Garnet

[Garnet](https://fuchsia.googlesource.com/garnet) はネットワークアクセスに必要な無線LANやBluetoothのドライバなどをはじめとするOSが必要とする低レベルなシステムサービスを提供する。GPUを用いたグラフィックレンダラーであるEscherや、ソフトウェアのパッケージ管理を行うAmber、[Xi](https://github.com/google/xi-editor/)というGoogle製エディタのエンジンなど、さまざまなものが含まれる。

### Peridot

[Peridot](https://fuchsia.googlesource.com/peridot) はフレームワークを担う部分。例としては、Story、ModuleといったFuchsiaのコンテキスト管理の仕組みやLedgerという分散ストレージの仕組みが含まれる。

### Topaz
[Topaz](https://fuchsia.googlesource.com/topaz)はもっとも上位の層で、メインのホームUIやその他のシステムアプリなどを提供する。Topazではアプリ開発の標準SDKとして [Flutter](https://flutter.io/)をサポートする。
