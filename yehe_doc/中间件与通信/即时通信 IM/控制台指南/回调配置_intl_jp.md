[IMコンソール](https://console.cloud.tencent.com/im)にログインし、対象のアプリケーションカードをクリックして、左側ナビゲーションバーで【コールバック設定】を選択します。実際の業務に応じてコールバックURLを設定し、有効にするコールバックを決定できます。

## コールバックURLの設定

1. 【コールバック設定】ページで、コールバックURL設定エリアの【編集】をクリックします。
2. ポップアップ表示されたコールバックURL設定のダイアログボックスに、コールバックURLを入力します。

>?
>- コールバックURLは、`http://`または`https://`で始まらなければなりません。
>- ドメイン名をまだ申請していない場合は、`http://123.123.123.123/imcallback`など、IPを直接設定することができます。
>- 使用できるのは、英語アルファベット（`a～z`、大文字と小文字は区別しません）、数字(0～9)およびハイフン(-)のみです。スペースや次の文字（！$&？など）はサポートされていません。
>- ハイフン(-)を連続して表示したり、単独で登録したり、先頭または末尾に配置したりすることはできません。  
>- ドメイン名の長さは63文字以下とします。
>- コールバックURLのIMのデフォルトは80/443ポートで、コールバックURLが置き換えられると、ポートに変更が生じます。置き換え前後のポートを相互にプレフィックスとして使用しないでください。例えば、https://xxx:443をhttps://xxx:4433に変更したり、https://xxxをhttps://xxx:4433に変更したりすることは避けてください。

3. 【OK】をクリックし、設定を保存します。

## イベントコールバックの設定
1. 【コールバックの設定】ページで、イベントコールバック設定エリアの【編集】をクリックします。
2. コールバックURLを設定するポップアップダイアログボックスで、必要なコールバックにチェックを入れます。
![](https://main.qcloudimg.com/raw/67cb8c9fd2365e3e2014e6940c468aaf.png)
3. 【OK】をクリックして設定を保存します。

## HTTPS双方向認証証明書のダウンロード
コールバックURLを設定すると、コンソールでHTTPS双方向認証証明書をダウンロードできます。
>?必要に応じて双方向認証を設定することができます。具体的な設定方法については、 [双方向認証の設定](https://intl.cloud.tencent.com/document/product/1047/34379)をご参照ください。

1.  [コンソール](https://console.cloud.tencent.com/im-detail/callback-setting) の【[コールバック設定](https://console.cloud.tencent.com/im-detail/callback-setting)】ページに進み、右上のコールバックURL設定エリアの【HTTPS双方向認証証明書のダウンロード】をクリックします。
![](https://main.qcloudimg.com/raw/52a1d6fc283f07e29842da512ba303a3.png)
2. ポップアップ表示された証明書ダウンロードのダイアログボックスで、【ダウンロード】をクリックします。
![](https://main.qcloudimg.com/raw/584dcfbed3a36a691971f6edcca19b43.png)
3. 証明書ファイルを保存します。


## 後続の操作
コールバックURLを設定し、対応するイベントコールバックを有効化した後、 [サードパーティのコールバック](https://intl.cloud.tencent.com/document/product/1047/34354)を参照して、対応するコールバック機能を使用すると、ユーザー情報と操作情報をリアルタイムで取得できます。
