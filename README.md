# ソラコムIoT SIM の Jetson へのセットアップ #

ソラコムIoT SIM および USBドングルをJetsonに対してセットアップする

OS: JetPack 4.X  
USBドングル: Huawei MS2372
 

### Huawei USBドングルのセットアップ ###

* HUAWEIのMS2372ドングルで初回使用の場合のみ以下の操作が必要
* 他の機種を使用する場合は別途手順を確認すること

```
$ sudo apt update  
$ sudo apt install screen  
$ sudo screen /dev/ttyUSB0 38400  
  
ATE1[Enter]
OK
AT+CGDCONT=0,"IP","soracom.io"[Enter]
OK
[Ctrl]+[A] → [K]
Really kill this window [y/n] y[Enter]
```

### 接続構成のセットアップ ###

* デバイス一覧を確認し、TYPEが"gsm"のものが接続されていることを確認する
```
$ nmcli device status
```
* 接続を実行する
```
$ sudo nmcli connection add type gsm ifname "*" con-name soracom apn soracom.io user sora password sora
```
* 正しく接続したことを確認する
```
$ nmcli device status
```
* CONNECTIONが"soracom"になっていればOK

### 次にやること ###

[check-usb-dongle-connection](https://github.com/latonaio/check-usb-dongle-connection)

* エッジ端末(Jetson)にてUSBドングルが正しく接続されているかどうかを確認するマイクロサービスのセットアップ


# その他 #
上記のほか、次の作業が必要になります。（状況に応じてNapter等の契約が必要な場合があります）

・Soracomへの管理者ログイン  
・SAMユーザーの作成  
・作成したSAMユーザーでログイン  
・sshでログイン  
・SIMがオンラインになっていることを確認する  
・オンデマンドリモートアクセスの選択  