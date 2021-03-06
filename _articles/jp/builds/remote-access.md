---
changelog: ''
last_modified_at: 
title: リモートアクセス
new_article: false
tag: []
summary: ''
menu:
  builds-main:
    weight: 34

---

リモートアクセスでは、SSHや画面共有アプリを介してビルドの仮想マシンに接続することができます。失敗したビルドはリモートアクセスを有効にして再構築することができ、トラブルシューティングを非常に簡単にすることができます。

{% include message_box.html type="important" title="Authorization" content="アプリ上で**テスター/QA**のロールを持っているユーザーは、リモートアクセスできません。"%}

ビルドマシンにリモートアクセスするには2つの方法があります。

* **SSH**: Linux/DockerベースのマシンとMacOSマシンの両方で利用できます。
* **画面共有**: MacOSマシンでしか使えません。

どちらの方法でも、ビルド中と、ビルド終了後の10分間はビルドマシンにリモートでアクセスできます。

## SSHによるリモートアクセス

1. ビルドページに移動します。
2. **Rebuild with Remote Access**オプションをクリックします。
3. **Remote Access Instructions**をクリックします。

   ![](/img/remote-access-instructions.png)
4. **SSH**オプションの下から必要なコマンドを探してコピーします。
5. コマンドラインインターフェースを開きます。
6. **SSH**の下にあるコマンドを実行します（以下は例です）。

       ssh -o StrictHostKeyChecking=no vagrant@1.tcp.ngrok.io -p 000000
7. **SSH**の下にあるパスワードをコピーして貼り付けます。

これで完了です。ビルドが実行されている仮想マシンにアクセスできるはずです。

## 画面共有によるリモートアクセス

1. ビルドページに移動します。
2. **Rebuild with Remote Access**オプションをクリックします。
3. **Remote Access Instructions**をクリックします。

   ![](/img/remote-access-instructions.png)
4. **Screenshare**オプションから以下のような情報を探します。
   * Address
   * Username
   * Password
5. 画面共有アプリケーションを開きます。
6. **Screenshare**オプションの情報を、画面共有アプリケーションの必要なフィールドに入力してください。

## リモートアクセス利用可能時間の拡大

リモートアクセスは、ビルド実行中とビルド終了後の10分間利用可能です。これでは不十分な場合は、リモートアクセスをより長い時間利用できるようにする簡単な回避策があります。

1. ビルドが失敗する原因となるステップの後に**Script**ステップを追加します。
2. **Run if previous Step failed**オプションをオンにすると、**Script**ステップが常に実行されるようになります。
3. 秒単位で指定した時間だけビルドをスリープさせるコマンドを追加します

   `1 sleep 5400`

   この例では、ビルドを90分間実行します。もちろん、ビルドの制限時間を超えてはいけません。

以上です。ビルドが実行されている間は、失敗の原因となった可能性のある問題を仮想マシン上で見て回ることができます。

これで完了です！ビルドが実行されている仮想マシンにアクセスできるようになりました。