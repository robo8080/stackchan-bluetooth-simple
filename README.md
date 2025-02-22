# stackchan-bluetooth-simple


---
mongonta0716さんの ｽﾀｯｸﾁｬﾝ Arduinoファームウェア”stackchan-bluetooth-simple”にレベルメーターやFaceチェンジ機能を追加ました(Core2のみ）。<br>
オリジナルはこちらです。<br>
<https://github.com/mongonta0716/stackchan-bluetooth-simple><br>

どーもくん (C)NHK・TYO の画像を使用しています。<br>

### 使い方 ###
* Bluetoothモード時レベルメーターを表示できます。
* レベルメーター表示部にタッチすると、レベルメーター表示をON/OFFできます。<br>
* レベルメーター表示OFFの時、画面下部にタッチするとバルーンで曲名を表示します。<br>
* 画面右端の中央付近にタッチするとFaceを切り替えられます。<br>
* 画面中央にタッチすると首振りを止めます。<br><br>

---


日本語 | [English](README_en.md)

# 概要

M5Stack-AvatarをベースにシンプルにBluetoothスピーカー機能とスタックチャンのサーボコントロール機能をつけました。
[M5Unified](https://github.com/m5stack/M5Unified)のexampleであるBluetooth_with_ESP32A2DPをベースに改造しています。


# 開発環境
- VSCode
- PlatformIO

# 対応機種

- ~~M5Stack Basic/Gray/M5Go<br>BasicはFlashメモリが16MBの機種のみです。~~

- ~~M5Stack Fire~~

- M5Stack Core2 / Core2 for AWSIoT

# 必要なライブラリ
Arduino-ESP32は2.0.4(Fireのみ2.0.0)で動作確認しています。~~M5Stack Fireはarduino-esp32v2.0.4だと不具合があり起動しません。~~

詳しいバージョンについては[platformio.ini](https://github.com/mongonta0716/stackchan-bluetooth-simple/blob/main/platformio.ini)を見てください。

- ~~[M5Stack-Avatar](https://github.com/meganetaaan/m5stack-avatar)~~

- [ServoEasing](https://github.com/ArminJo/ServoEasing)

- [ESP32Servo](https://github.com/madhephaestus/ESP32Servo)

- [M5Unified](https://github.com/m5stack/M5Unified)

- [ESP8266Audio](https://github.com/earlephilhower/ESP8266Audio)

- [ESP32-A2DP](https://github.com/pschatzmann/ESP32-A2DP)

- [ArduinoJson](https://github.com/bblanchon/ArduinoJson)

- [YAMLDuino](https://github.com/tobozo/YAMLDuino)

# コンパイル時の注意

- ~~M5Stack Fire V2.6/M5Stack Basic V2.6<br>TFカードを使用する際にSD.begin()を20MHz以上では読み込めない事象を確認しました。15MHzに下げています。~~

- ~~M5Stack Basic V2.6<br>VSCode+PlatformIOでコンパイルするときのenvは`env:m5stack-grey`を選択してください。~~

# 設定
SDカードに設定用のYAMLファイルがないとデフォルト値を利用します。（PortAへサーボを接続する設定になっています。）
SDカードに`/yaml/SC_Config.yaml`を配置すると自分の設定が利用できます。

**2022/10/18にJSONからYAMLへ変更しました。JSONからYAMLへのコンバートは[JSON から YAML コンバータ](https://www.site24x7.com/ja/tools/json-to-yaml.html)にて可能です。**<br>コメントの扱いが変わっているので注意してください。

詳しくは[YAMLファイル](https://github.com/mongonta0716/stackchan-bluetooth-simple/blob/main/data/yaml/SC_Config.yaml)を参照してください。

## 設定項目
(カッコ内)は初期値
- servo
    - pin
        - x(Core1 22, Core2 33)<br> X軸のGPIOを指定
        - y(Core1 21, Core2 32)<br> Y軸のGPIOを指定
    - offset<br>サーボの軸が90°にしたときにズレを修正するパラメータ
        - x(0)<br> X軸のオフセット値を設定
        - y(0)<br> Y軸のオフセット値を設定

    - speed<br>待機時とBluetoothスピーカーで音が出ているときの待機時間とサーボの移動時間を指定します。最小値と最大値で範囲を指定して、ランダムの値を使用します。
        - normal_mode
             - interval_min(5000)
             - interval_max(10000)
             - move_min(500)
             - move_max(1500)
        - sing_mode
             - interval_min(1000)
             - interval_max(2000)
             - move_min(500)
             - move_max(1500)
- bluetooth
    - device_name(M5Stack_BTSPK)<br>Bluetoothスピーカーのデバイス名を指定します。
    - starting_state(false)<br>起動時にBluetoothモードにするかどうかを指定します。
    - start_volume(100)<br>Bluetoothスピーカーの初期値を設定

- auto_power_off_time(0)<br>Core2のみ。USBの電源供給がOFFになったあと設定した時間が経過すると電源OFFになります。（0は電源OFFしない）

- balloon<br>吹き出しの設定をします。
    - font_language("JA")<br>フォントの言語を指定します。"JA"か"CN"、指定しないとラテンフォントを使用します。
    - lyrics("こんにちは",”Hello”,"你好","Bonjour")<br>ノーマルモード時にランダムで表示するセリフを設定します。最大10個まで。

# 使い方

- BtnA<br>Bluetoothモードに入ります。(bluetooth_mode = falseの時のみ有効)<br>

- BtnB<br>音量を下げます。

- BtnC<br>音量を上げます。

# Credit
- [meganetaaan](https://github.com/meganetaaan)
- [lovyan03](https://github.com/lovyan03/LovyanGFX)
- [robo8080](https://github.com/robo8080)
- [tobozo](https://github.com/tobozo)

# LICENSE
[MIT](LICENSE)

# Author
[Takao Akaki](https://github.com/mongonta0716)



