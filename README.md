
# LAN内通知の極意：KDE Connectでコマンド終了を通知

![](assets/eye-catch.png)

## はじめに
KDE Connectは、UbuntuなどのLinuxデスクトップとAndroidスマートフォンを連携させるアプリケーションです。
ファイルの共有、クリップボードの共有、通知の同期、さらにはリモートコントロールなど、多岐にわたる機能を提供します。

例えば長時間実行するスクリプトが終了した際に、LAN内のスマートフォンに通知を送ることが可能です。

サーバーのバックアップ完了通知やシステムメンテナンスの完了アラートなど、様々なシナリオで役立つと思います。

## 他の方法
LAN外であれば、以下の記事が参考になるでしょう。
[Androidに通知を送るのにntfy.shが便利だった](https://zenn.dev/tantan_tanuki/articles/06d2b714d88df0)

わたしの場合は、LAN内での通知が必要だったので、KDE Connectを使うことにしました。

## KDE Connectの基本設定

### KDE Connectのインストール方法
KDE Connectを使用するための最初のステップは、当然ながら、アプリケーションのインストールです。ここでは、UbuntuおよびAndroidスマートフォンでのインストール手順について説明します。

#### Ubuntuでのインストール
Ubuntu環境にKDE Connectをインストールするには、次のコマンドをターミナルで実行します。
```bash
sudo apt update
sudo apt install kdeconnect -y
```
このコマンドにより、最新のKDE Connectがシステムにインストールされます。

#### スマートフォンでのインストール
AndroidスマートフォンにKDE Connectをインストールするには、Google Playストアを利用します。Playストアを開いて「KDE Connect」と検索し、アプリを選択して「インストール」をタップします。

### デバイス間のペアリング方法
インストールが完了したら、次はUbuntuとスマートフォンのペアリングを行います。これにより、デバイス間での通信が可能になります。

1. **Ubuntu側での設定**: UbuntuにインストールしたKDE Connectを開きます。アプリケーションは、システムトレイまたはアプリケーションメニューからアクセスできます。

2. **スマートフォン側での設定**: スマートフォンでKDE Connectアプリを開きます。ここで、同じWi-Fiネットワークに接続されていることを確認してください。

3. **ペアリングの開始**: Ubuntu側で利用可能なデバイスのリストが表示されるので、ペアリングしたいスマートフォンを選択し、「ペアリング」をクリックします。

4. **ペアリングの承認**: スマートフォン側でペアリングリクエストが表示されるので、「承認」を選択します。

以上で、UbuntuとスマートフォンがKDE Connectを通じてペアリングされます。このペアリングが成功すると、デバイス間でファイルの転送、通知の同期、さらには本ブログで重点を置いているSMSの送信や電話のベル操作など、多様な機能が利用可能になります。

## KDE Connectを使ったSMS送信

KDE Connectは、スマートフォンの機能を直接コントロールする強力なコマンドラインツール `kdeconnect-cli` を提供します。このツールを使用して、簡単にSMSを送信することができます。これは特に、重要なタスクやアラートが完了した際に自動的に通知を送りたい場合に便利です。

### `kdeconnect-cli --send-sms` コマンドの使用方法
SMSを送信するための基本的なコマンドは次のようになります：
```bash
kdeconnect-cli --send-sms "メッセージ内容" --destination "送信先の電話番号" -n "デバイス名"
```
ここで、`--send-sms` は送信するメッセージを指定し、`--destination` で送信先の電話番号を指定し、`-n` は使用するデバイス（スマートフォン）の名前を指定します。

### 実際のコマンド例とその説明
例えば、電話番号「1234567890」に「こんにちは」というメッセージを送る場合、コマンドは次のようになります：
```bash
kdeconnect-cli --send-sms "こんにちは" --destination "1234567890" -n "あなたのデバイス名"
```
このコマンドを実行すると、指定された電話番号に「こんにちは」というメッセージが送信されます。

### 利用シナリオ：タスクの完了やアラートをSMSで通知
この機能の一つの利用シナリオは、長時間かかるスクリプトやプロセスが完了した際に通知を受け取ることです。例えば、サーバーのバックアップが完了した後に「バックアップ完了」というメッセージを自分の電話に自動的に送信するように設定できます。

スクリプトやプログラムの最後に上記のコマンドを追加するだけで、プロセスの完了通知を手軽に受け取ることが可能になります。これにより、リアルタイムでの進捗監視が不要となり、作業効率が大幅に向上します。

## スマートフォンのベルを鳴らす

KDE Connectには、スマートフォンのベルを鳴らすための便利な機能があります。この機能は、`kdeconnect-cli` コマンドラインツールを使用してアクセスでき、特定のイベントやタスクが完了したときにスマートフォンで物理的なアラートを生成するのに役立ちます。

### `kdeconnect-cli --ring` コマンドの使用方法
スマートフォンのベルを鳴らすためには、以下のコマンドを使用します：
```bash
kdeconnect-cli --ring -n "デバイス名"
```
このコマンドでは、`--ring` オプションがスマートフォンのベルを鳴らすために使用され、`-n` オプションで対象のデバイス名を指定します。

### 実際のコマンド例とその説明
例えば、デバイス名が「MAR-LX2J」のスマートフォンのベルを鳴らしたい場合、次のようなコマンドを使用します：
```bash
kdeconnect-cli --ring -n "MAR-LX2J"
```
このコマンドを実行すると、指定されたデバイスのベルが鳴ります。

### 利用シナリオ：特定のイベントやタスク完了時にスマートフォンのベルを鳴らす
この機能は、特にサーバーやバックグラウンドで実行中のプロセスが完了したときに非常に便利です。例えば、重要なデータのダウンロードが完了したり、システムのメンテナンスが終了したりしたときに、スマートフォンで物理的な通知を受け取ることができます。

スクリプトやコマンドラインプロセスの最後にこのコマンドを追加することで、プロセスの完了を即座に知ることができます。これにより、デスクトップの前に座っていなくても、重要なタスクの完了を確実に把握することが可能になります。

## 実践的な使用例

KDE Connectを使用して、スクリプトやシステムコマンドの完了時にSMS通知を送るか、またはスマートフォンのベルを鳴らすことは、効率的なワークフローを構築する上で非常に有効です。以下に、このような利用シナリオの具体的な例をいくつか挙げます。

### スクリプト完了時のSMS通知
ある長時間実行されるスクリプトが完了したときに、自動的にSMS通知を送信する例を考えてみましょう。以下は、スクリプトが完了した際に「スクリプト完了」というメッセージを送信するコマンドの例です。

```bash
# スクリプトやコマンドの実行
# ...

# スクリプト完了後にSMSを送信
kdeconnect-cli --send-sms "スクリプト完了" --destination "あなたの電話番号" -n "あなたのデバイス名"
```

### バックアップ完了通知
サーバー上でバックアッププロセスが完了した際に、スマートフォンに「バックアップ完了」というメッセージを送る場合、次のようにコマンドを設定します。

```bash
# バックアッププロセスの実行
# ...

# バックアップ完了後にSMSを送信
kdeconnect-cli --send-sms "バックアップ完了" --destination "あなたの電話番号" -n "あなたのデバイス名"
```

### サーバーメンテナンスの完了通知
サーバーメンテナンスが完了した際に、スマートフォンのベルを鳴らすことで通知する場合は、以下のようなコマンドを使用します。

```bash
# メンテナンスプロセスの実行
# ...

# メンテナンス完了後にスマートフォンのベルを鳴らす
kdeconnect-cli --ring -n "あなたのデバイス名"
```

これらの例は、KDE Connectを使用して、重要なプロセスの完了をリアルタイムで通知するための方法を示しています。これにより、ユーザーはデスクトップの前にいなくても、重要なイベントの完了を確実に知ることができるようになります。

## セキュリティと制限事項

KDE Connectは非常に便利なツールですが、セキュリティ面での考慮事項やいくつかの制限があります。これらを理解し、適切に対処することで、安全かつ効率的にKDE Connectを利用できます。

### KDE Connectのセキュリティ面についての考慮事項
1. **プライベートネットワークの使用**：KDE Connectは、デバイス間の通信にローカルネットワークを使用します。そのため、公共のWi-Fiネットワークではなく、信頼できるプライベートネットワーク上で使用することが重要です。

2. **ファイアウォールとセキュリティ設定**：ファイアウォールやセキュリティソフトウェアがKDE Connectの機能を妨げる可能性があるため、適切な設定が必要です。特定のポートを開放することで、通信の安定性を確保します。

3. **アプリケーションの更新**：セキュリティの脆弱性を最小限に抑えるためには、常に最新のバージョンのKDE Connectを使用することが推奨されます。

### 制限事項とトラブルシューティングのヒント
1. **デバイスの互換性**：全ての機能がすべてのデバイスやオペレーティングシステムでサポートされているわけではありません。特に古いデバイスやOSでは、一部の機能が制限される可能性があります。

2. **ネットワークの制約**：KDE Connectは同じネットワーク上のデバイス間でのみ機能します。異なるネットワーク上では使用できないことに注意してください。

3. **トラブルシューティング**：接続に問題がある場合は、両デバイスの再起動やネットワーク設定の確認を行います。また、KDE Connectの設定を再確認し、必要に応じてペアリングをやり直してみてください。

## 参考文献
1. **KDE Connect公式ウェブサイト**：
   - [KDE Connect - KDE.org](https://kdeconnect.kde.org/)
   こちらはKDE Connectの公式ウェブサイトで、基本情報、機能紹介、ダウンロードリンクなどが提供されています。

2. **KDE Connectユーザーガイド**：
   - [KDE Connect - User Documentation](https://userbase.kde.org/KDEConnect)
   KDE Connectの使い方に関する詳細なガイドが提供されています。初心者から上級ユーザーまで役立つリソースです。

3. **KDE Connect GitHubリポジトリ**：
   - [KDE Connect on GitHub](https://github.com/KDE/kdeconnect-kde)
   開発者のためのリポジトリですが、ソースコードや開発に関する最新の情報を得ることができます。

4. **コミュニティフォーラムとサポート**：
   - [KDE Forums - KDE Connect](https://forum.kde.org/viewforum.php?f=83)
   KDE Connectに関する疑問や問題を共有し、コミュニティのサポートを受けることができるフォーラムです。

```bash
使い方: kdeconnect-cli [オプション]
KDE Connect CLI tool

オプション:
  -l, --list-devices            List all devices
  -a, --list-available          List available (paired and reachable) devices
  --id-only                     Make --list-devices or --list-available print
                                only the devices id, to ease scripting
  --name-only                   Make --list-devices or --list-available print
                                only the devices name, to ease scripting
  --id-name-only                Make --list-devices or --list-available print
                                only the devices id and name, to ease scripting
  --refresh                     Search for devices in the network and
                                re-establish connections
  --pair                        Request pairing to a said device
  --ring                        Find the said device by ringing it.
  --unpair                      Stop pairing to a said device
  --ping                        Sends a ping to said device
  --ping-msg <message>          Same as ping but you can set the message to
                                display
  --share <path>                Share a file to a said device
  --share-text <text>           Share text to a said device
  --list-notifications          Display the notifications on a said device
  --lock                        Lock the specified device
  --send-sms <message>          Sends an SMS. Requires destination
  --destination <phone number>  Phone number to send the message
  --device, -d <dev>            Device ID
  --name, -n <name>             Device Name
  --encryption-info             Get encryption info about said device
  --list-commands               Lists remote commands and their ids
  --execute-command <id>        Executes a remote command by id
  -k, --send-keys <key>         Sends keys to a said device
  --my-id                       Display this device's id and exit
  --photo <path>                Open the connected device's camera and transfer
                                the photo
  -h, --help                    このヘルプを表示する。
  -v, --version                 バージョン情報を表示する。
  --author                      Show author information.
  --license                     ライセンス情報を表示
  --desktopfile <ファイル名>         The base file name of the desktop entry for
                                this application.

```