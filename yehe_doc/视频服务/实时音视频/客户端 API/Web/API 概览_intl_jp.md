## サポートするプラットフォーム

WebRTCのテクノロジーはGoogleが初めて提唱し、現在、デスクトップ版Chromeブラウザ、デスクトップ版Edgeブラウザ、デスクトップ版Firefoxブラウザ、デスクトップ版Safariブラウザおよびモバイル版Safariブラウザでは比較的万全なサポートが提供されています。その他のプラットフォーム（Androidプラットフォームブラウザなど）のサポート状況は未だ不十分です。

お客様のユースケースが主に教育シーンである場合、教師用端末はより安定性の高い[Electron](https://intl.cloud.tencent.com/document/product/647/35097)ソリューションを使用することをお勧めします。このソリューションは、大小のデュアルチャネル画面、より柔軟性の高い画面共有ソリューションおよび脆弱なネットワークに対する高い回復力をサポートしています。

<table>
<tr>
<th>OS</th>
<th>ブラウザタイプ</th>
<th>ブラウザの最小<br>バージョン要件</th>
<th>SDKのバージョン要件</th>
<th>受信（再生）</th>
<th>送信（マイク・オン）</th>
<th>画面共有</th>
</tr>
<tr>
<td rowspan="11">Windows</td>
<td>デスクトップ版Chromeブラウザ</td>
<td>56+</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしています（Chrome72+バージョンが必要）</td>
</tr>
<tr>
<td>デスクトップ版QQブラウザ（クイックコア）</td>
<td>10.4+</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>デスクトップ版Firefoxブラウザ</td>
<td>56+</td>
<td>v4.7.0+</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしています（Firefox66+バージョンが必要）</td>
</tr>
<tr>
<td>デスクトップ版Edgeブラウザ</td>
<td>80+</td>
<td>v4.7.0+</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしています</td>
</tr>
<tr>
<td>デスクトップ版Sogouブラウザ（高速モード）</td>
<td>11+</td>
<td>v4.7.0+</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしています</td>
</tr>
<tr>
<td>デスクトップ版Sogouブラウザ（互換モード）</td>
<td>-</td>
<td>-</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>デスクトップ版Operaブラウザ</td>
<td>46+</td>
<td>v4.7.0+</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしています（Opera60+バージョンが必要）</td>
</tr>
<tr>
<td>デスクトップ版360SEブラウザ（超高速モード）</td>
<td>13+</td>
<td>v4.7.0+</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしています</td>
</tr>
<tr>
<td>デスクトップ版360SEブラウザ（互換モード）</td>
<td>-</td>
<td>-</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>デスクトップ版WeChat Embeddedブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>デスクトップ版WeCom Embeddedブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
</tr>
<tr>
<td rowspan="7">Mac OS</td>
<td>デスクトップ版Safariブラウザ</td>
<td>11+</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしています（Safari13+バージョンが必要）</td>
</tr>
<tr>
<td>デスクトップ版Chromeブラウザ</td>
<td>56+</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしています（Chrome72+バージョンが必要）</td>
</tr>
<tr>
<td>デスクトップ版Firefoxブラウザ</td>
<td>56+</td>
<td>v4.7.0+</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしています（Firefox66+バージョンが必要）</td>
</tr>
<tr>
<td>デスクトップ版Edgeブラウザ</td>
<td>80+</td>
<td>v4.7.0+</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしています</td>
</tr>
<tr>
<td>デスクトップ版Operaブラウザ</td>
<td>46+</td>
<td>v4.7.0+</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしています（Opera60+バージョンが必要）</td>
</tr>
<tr>
<td>デスクトップ版WeChat Embeddedブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>デスクトップ版WeCom Embeddedブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
</tr>
<tr>
<td rowspan="6">Android</td>
<td>WeChat Embeddedブラウザ（TBSコア）</td>
<td>-</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>WeChat Embeddedブラウザ（XWEBコア）</td>
<td>-</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>WeCom Embeddedブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>モバイル版Chromeブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>モバイル版QQブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>モバイル版UCブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>iOS 12.1.4+</td>
<td>WeChat Embeddedブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>iOS 14.3+</td>
<td>WeChat Embeddedブラウザ</td>
<td>6.5+（WeChatバージョン）</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>iOS</td>
<td>WeCom Embeddedブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>iOS 11.1.2+</td>
<td>モバイル版Safariブラウザ</td>
<td>11+</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>iOS 12.1.4+</td>
<td>モバイル版Chromeブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>iOS 14.3+</td>
<td>モバイル版Chromeブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしていません</td>
</tr>
</table>

>! 
>- ブラウザで[WebRTC能力テスト](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)画面を開けば、例えば、公式アカウントなどのブラウザ環境など、WebRTCが完全にサポートされているかどうかチェックすることができます。
>- H.264版の権限の制限によって、HuaweiシステムのChromeブラウザおよびChrome WebViewをコアとするブラウザでは、TRTCデスクトップブラウザSDKの正常動作をサポートしていません。

## API使用ガイド
APIの使用法の詳細については、以下のガイドをご参照ください。

| 機能    | Sample Codeガイド       |
| -------------------------- | ---------------------------------------------- |
| 基本的なオーディオビデオ通話     | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-11-basic-video-call.html)           |
| インタラクティブライブストリーミング                   | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-12-basic-live-video.html)    |
| カメラおよびマイクの切り替え         | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-13-basic-switch-camera-mic.html)    |
| ローカルビデオのプロパティの設定           | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-14-basic-set-video-profile.html)    |
|ローカルオーディオまたはビデオの動的な停止｜ [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-15-basic-dynamic-add-video.html)    |
| 画面共有                   | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-16-basic-screencast.html)           |
| 音量計測       | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-17-basic-detect-volume.html)        |
| ユーザー定義キャプチャとカスタマイズ再生レンダリング | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-20-advanced-customized-capture-rendering.html) |
| ルーム内アップリンクユーザー数の制限     | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-04-info-uplink-limits.html)        |
| バックグラウンドミュージックと効果音の実装ソリューション     | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-22-advanced-audio-mixer.html)                  |


## TRTC

>!このドキュメントは4.x.xバージョンのTRTC Web SDKに適用されます。

TRTCは[TRTC Web SDK](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/index.html)のメインエントリで、TRTCメソッドによってTRTCのクライアントオブジェクト（Client）とローカルオーディオビデオストリーミングオブジェクト（Stream）を作成することができます。また、TRTCメソッドはブラウザの互換性や、画面共有をサポートするかをチェックしたり、ログレベルやログのアップロードを設定したりすることもできます。

| API               | 説明               |
| ----------------------------------------- | ---------------------------------------- |
| [VERSION](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.VERSION)         | TRTC Web SDKバージョン番号。           |
| [checkSystemRequirements](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.checkSystemRequirements) | ブラウザがTRTC Web SDKと互換性があるかチェックします。現在のブラウザとTRTC Web SDKとの互換性がない場合は、Chromeブラウザの最新バージョンをダウンロードすることをお勧めします。          |
| [isScreenShareSupported](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.isScreenShareSupported)   | ブラウザが画面共有をサポートするかチェックします。画面共有ストリームを作成する前に、このメソッドを呼び出して、現在のブラウザが画面共有をサポートするか確認してください。|
| [getDevices](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.getDevices)           | メディアの入出力デバイスリストを返します。             |
| [getCameras](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.getCameras)           | カメラのデバイスリストを返します。          |
| [getMicrophones](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.getMicrophones)           | マイクのデバイスリストを返します。          |
| [getSpeakers](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.getSpeakers)         | スピーカーのデバイスリストを返します。          |
| [createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createClient)    |TRTC通話のクライアントオブジェクトを作成します。セッションごとに一度だけ呼び出す必要があります。          |
| [createStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createStream)    | ローカルストリームStreamオブジェクトを作成します。ローカルストリームStreamオブジェクトは[publish()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#publish)メソッドによってオーディオビデオストリーミングをリリースします。 |

## TRTC.Logger

[ログ出力レベル](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.Logger.html#.LogLevel)の設定を含め、ログの設定方法を提供します。ログのアップロードを起動または停止します。

| API        | 説明       |
| ---------------------------------- | ------------------ |
|  [setLogLevel](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.Logger.html#.setLogLevel)           | ログ出力レベルを設定します。 |
| [enableUploadLog](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.Logger.html#.enableUploadLog)   | ログのアップロードを起動します。     |
| [disableUploadLog](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.Logger.html#.disableUploadLog) | ログのアップロードを停止します。     |

## Client

オーディオビデオ通話のクライアントオブジェクトClientは[createClient()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createClient)によって作成し、オーディオビデオセッションを代表します。

| API        | 説明         |
| ---------------------------------- | ---------------------------------------------------------- |
| [setProxyServer](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#setProxyServer)           | プロキシサーバーを設定します。このメソッドは、nginx+coturn方式など、企業が自分でプロキシサーバーをデプロイする場合に適用されます。       |
| [setTurnServer](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#setTurnServer)     | TURNサーバーを設定します。このメソッドは[setProxyServer()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#setProxyServer)と合わせて使用し、企業が自分でプロキシサーバーおよびTURN中継をデプロイする場合に適用されます。 |
| [join](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#join)       | オーディオビデオ通話ルームに参加し、入室によってオーディオビデオ通話セッションが始まります。ルームが存在しない場合、システムが自動的に新しいルームを作成します。            |
| [leave](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#leave)     | 現在のオーディオビデオ通話ルームを退出し、オーディオビデオ通話セッションを終了します。         |
| [publish](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#publish)         | ローカルのオーディオビデオストリーミングを公開します。このメソッドは[join()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#join) で入室後に呼び出す必要があり、1回のオーディオビデオセッションで1度だけローカルストリーミングを公開することができます。           |
| [unpublish](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#unpublish)          | ローカルストリーミングの公開を取り消します。     |
| [subscribe](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#subscribe)          | リモートストリーミングを閲覧します。         |
| [unsubscribe](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#unsubscribe)         | リモートストリーミングの閲覧を取り消します。     |
| [switchRole](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#switchRole)           | ユーザーロールを切り替えます。‘live’でインタラクティブライブストリーミングモードの時のみ有効になります。           |
| [on](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#on)           | クライアントオブジェクトイベントを監視します。         |
| [getRemoteMutedState](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#getRemoteMutedState) | 現在のルーム内にいるリモートユーザーのオーディオビデオのmute状態リストを取得します。             |
| [getLocalAudioStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#getLocalAudioStats)   | 現在公開済みのローカルストリーミングのオーディオ統計データを取得します。このメソッドは[publish()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#publish)後に呼び出す必要があります。           |
| [getLocalVideoStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#getLocalVideoStats)   | 現在公開済みのローカルストリーミングのビデオ統計データを取得します。このメソッドは[publish()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#publish)後に呼び出す必要があります。           |
| [getRemoteAudioStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#getRemoteAudioStats) | 現在のすべてのリモートストリーミングのオーディオ統計データを取得します。           |
|  [getRemoteVideoStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#getRemoteVideoStats) | 現在のすべてのリモートストリーミングのビデオ統計データを取得します。           |

## LocalStream

LocalStreamローカルオーディオビデオストリーミングは、[createStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createStream)で作成します。[Stream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Stream.html)のサブカテゴリーになります。

| API             | 説明               |
| --------------------------------------- | ------------------------------------------ |
| [initialize](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#initialize)           | ローカルのオーディオビデオストリーミングオブジェクトを初期化します。      |
| [setAudioProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#setAudioProfile)         | オーディオProfileを設定します。このメソッドは[initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#initialize)を呼び出す前に呼び出す必要があります。          |
| [setVideoProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#setVideoProfile)         | ビデオProfileを設定します。このメソッドは[initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#initialize)を呼び出す前に呼び出す必要があります。          |
| [setScreenProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#setScreenProfile)         | 画面共有Profileを設定します。このメソッドは[initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#initialize)を呼び出す前に呼び出す必要があります。         |
| [setVideoContentHint](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#setVideoContentHint) | ビデオコンテンツのヒントを設定します。主に、さまざまなシーンにおけるビデオコーデック品質の向上に用いられます。このメソッドは[initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#initialize)の呼び出し完了後に呼び出す必要があります。 |
| [switchDevice](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#switchDevice)       | メディアの入力デバイスを切り替えます。            |
| [addTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#addTrack)    | オーディオまたはビデオのトラックを追加します。          |
| [removeTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#removeTrack)         | ビデオトラックを削除します。        |
| [replaceTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#replaceTrack)       | オーディオまたはビデオのトラックを変更します。          |
| [play](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#play)       | このオーディオビデオストリーミングを再生します。              |
| [stop](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#stop)       | オーディオビデオストリーミングの再生を停止します。            |
| [resume](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#resume)           | オーディオビデオの再生を再開します。              |
| [close](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#close)     | オーディオビデオストリーミングを終了します。        |
| [muteAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#muteAudio)          | オーディオトラックを無効にします。        |
| [muteVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#muteVideo)          | ビデオトラックを無効にします。        |
| [unmuteAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#unmuteAudio)          | オーディオトラックを有効にします。        |
| [unmuteVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#unmuteVideo)         | ビデオトラックを有効にします。        |
| [getId](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#getId)     | Streamの固有識別IDを取得します。     |
| [getUserId](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#getUserId)          | このストリームが属するユーザーIDを取得します。       |
| [setAudioOutput](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#setAudioOutput)           | 音声出力デバイスを設定します。            |
| [getAudioLevel](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#getAudioLevel)     | 現在の音量を取得します。ローカルストリーミングまたはリモートストリーミングにオーディオデータがある場合のみ有効となります。        |
| [hasAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#hasAudio)    | オーディオトラックが含まれているかどうか。            |
| [hasVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#hasVideo)    | ビデオトラックが含まれているかどうか。            |
| [getAudioTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#getAudioTrack)     | オーディオトラックを取得します。        |
| [getVideoTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#getVideoTrack)     | ビデオトラックを取得します。        |
| [getVideoFrame](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#getVideoFrame)     | 現在のビデオフレームを取得します。              |
| [on](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#on)           | Streamイベントを監視します。            |



## RemoteStream

リモートオーディオビデオストリーミングは、[Client.on('stream-added')](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-Event.html#.STREAM_ADDED)イベントの監視によって取得します。これは[Stream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Stream.html)のサブカテゴリーになります。

| API    | 説明           |
| ------------------------------ | --------------------------- |
| [getType](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#getType)       | リモートストリーミングのタイプを取得します。主に1つのリモートストリーミングがメインオーディオビデオストリーミングかサブビデオストリームかを判断することに用いられます。サブビデオストリームは通常、画面共有ストリームです。 |
| [play](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#play)       | このオーディオビデオストリーミングを再生します。    |
| [stop](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#stop)       | オーディオビデオストリーミングの再生を停止します。          |
| [resume](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#resume)           | オーディオビデオの再生を再開します。    |
| [close](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#close)           | オーディオビデオストリーミングを終了します。      |
| [muteAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#muteAudio)           | オーディオトラックを無効にします。        |
| [muteVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#muteVideo)           | ビデオトラックを無効にします。        |
| [unmuteAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#unmuteAudio)           | オーディオトラックを有効にします。        |
| [unmuteVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#unmuteVideo)           | ビデオトラックを有効にします。        |
| [getId](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#getId)     | Streamの固有識別IDを取得します。     |
| [getUserId](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#getUserId)           | このストリームが属するユーザーIDを取得します。        |
| [setAudioOutput](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#setAudioOutput) | 音声出力デバイスを設定します。          |
| [setAudioVolume](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#setAudioVolume) | 再生音量を設定します。          |
| [getAudioLevel](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#getAudioLevel)   | 現在の音量を取得します。ローカルストリーミングまたはリモートストリーミングにオーディオデータがある場合のみ有効となります。      |
| [hasAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#hasAudio)     | オーディオトラックが含まれているかどうか。          |
| [hasVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#hasVideo)     | ビデオトラックが含まれているかどうか。          |
| [getAudioTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#getAudioTrack)     | オーディオトラックを取得します。      |
| [getVideoTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#getVideoTrack)     | ビデオトラックを取得します。      |
| [getVideoFrame](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#getVideoFrame)     | 現在のビデオフレームを取得します。    |
| [on](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#on)         | Streamイベントを監視します。          |


## RtcError

RtcErrorエラーオブジェクト。

| API          | 説明         |
| ------------------------------------- | ------------ |
| [getCode](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RtcError.html#getCode) | エラーコードを取得します。 |



## お問い合わせ

ご不明な点がございましたら、colleenyu@tencent.comにご連絡ください。
