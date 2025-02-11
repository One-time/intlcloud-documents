## サポートプラットフォーム

次のプラットフォームはすべて相互運用性をサポートしており、クロスターミナルのフルプラットフォームサービスを提供することができます。

| プラットフォーム    | SDKと互換性  | Demo     | ソースコード     | UIコンポーネント  |
| ------- | --------------| -------- | -------- | -------- |
| Android | JDK1.6およびAndroidSDKバージョン14以降のシステムと互換性があります | サポートあり     | サポートあり     | サポートあり     |
| iOS     | iOS8.0以降と互換性があります  | サポートあり     | サポートあり     | サポートあり     |
| Mac     | OS X10.10以降のバージョンと互換性があります  | サポートあり     | サポートあり     | -     |
| Windows | C、C ++を含み、Windows 7、Windows 8/8.1、Windows 10と互換性があり、32ビットおよび64ビットのプログラムアクセスを全面的にサポートします | - | - | - |
| Web     | IE 11以降、Chrome 7以降、FireFox 3.6以降、Opera 12以降、Safari6以降をサポートします  | サポートあり     | - | - |
| ミニプログラム  | サポートあり   | サポートあり     | - | - |
|Unity|2020.2.7f1c1以降のバージョンをサポートします|サポートあり|サポートあり|-|
|Flutter|Flutter 2.0.12バージョンをサポートします|サポートあり|サポートあり|-|
|Electron|サポートあり|サポートあり|サポートあり|-|

### グローバルアクセス

| 機能タイプ     | 機能の説明    |
| -------------- | -------------- |
| グローバルアクセスの概要   | IMは、全世界をカバーし、コネクティビティと信頼性が高く、強力なセキュリティを備えたネットワーク接続チャネルを提供し、自社開発した最適な多重アドレッシングアルゴリズムにより、ネットワーク全体のスケジューリング機能も有しています。海外の端末からログインすると、IM SDKが最寄りのアクセスポイントまたはアクセラレーションポイントにアクセスします|
| 中国 | 華南、華北、華東、中国香港、台湾など |
| 海外 | アジア：日本、韓国、シンガポール、インド、タイ、マレーシア、ベトナム、フィリピン、アラブ首長国連邦、インドネシア<br>ヨーロッパ：ドイツ、イギリス、フランス、ロシア、イタリア、ノルウェー、スペイン、オランダ<br>北米：アメリカ、カナダ、メキシコ<br>南アメリカ：ブラジル<br>オセアニア：オーストラリア<br>アフリカ：南アフリカ、ナイジェリアなど |


### アカウント機能

| 機能タイプ     | 機能の説明                               |
| ------------ | -------------------------------------- |
| アカウントインポート     | アカウント一括インポート                           |
| アカウント無効化     | UserSig無効化                           |
| アカウント削除     | アカウント一括削除                       |
| ユーザーオンラインステータス | オンラインおよびオフラインのステータスを管理（ユーザーがログインしていることが前提） |
| アカウントクエリ | アカウントがインポートされているかどうかの一括照会 |

### マルチ端末ログイン

| 機能タイプ      | 機能の説明                                                      |
| --------- | --------------------------------------------------------- |
| 同一プラットフォームログイン     | Android、iPhone、iPad、Windows、Mac、Webは1種類のプラットフォームのみオンライン可能             |
| デュアルプラットフォームログイン（デフォルト） | Android、iPhone、iPad、Windows、Macは1つの端末がオンライン可能。Webも同時オンライン可能            |
| トリプルプラットフォームログイン     | Android、iPhone、iPadは1種類のプラットフォームがオンライン可能。Windows、Macは1種類のプラットフォームがオンライン可能。Webも同時オンライン可能 |
| マルチプラットフォームログイン     |Android、iPhone、iPad、Windows、Mac、Webは全プラットフォームが同時オンライン可能              |

>?[IMコンソール](https://console.cloud.tencent.com/im)にログインし、ターゲットのアプリケーションが配置されている行の【アプリケーション設定】をクリックして、【機能設定】ページでマルチ端末ログインを設定します。

## メッセージタイプ

| 機能タイプ     | 機能の説明        |
| ------------ | ----------------- |
| テキストメッセージ     | メッセージの内容は通常のテキストです     |
| 画像メッセージ     | メッセージの内容は、画像のURLアドレス、サイズ、画像サイズなどの情報です    |
| 顔絵文字メッセージ     |顔絵文字メッセージは開発者向けにカスタマイズされています   |
| 音声メッセージ     | 音声データは秒単位で時間の長さ情報を提供する必要があります   |
| 地理的位置メッセージ | メッセージの内容は、地名、経度、緯度の情報です   |
| ファイルメッセージ     | メッセージの内容は、ファイルのURLアドレス、サイズ、形式などの情報であり、形式に制限はなく、最大100Mをサポートします |
| UGSVメッセージ   | メッセージの内容は、ファイルのURLアドレス、長さ、サイズ、形式などの情報で、最大100Mをサポートします                |
| カスタムメッセージ   | Red Packetメッセージ、ジャンケンなど、開発者がカスタマイズしたメッセージタイプです |
| システム通知メッセージ | 内蔵されているシステム通知メッセージと開発者がカスタマイズしたシステム通知メッセージがあります             |
|グループTipsメッセージ|グループに出入りするメンバー、グループの説明情報の変更、グループメンバープロファイルの変更など、システムの通知メッセージです|
|メッセージのマージ|最大300メッセージのマージをサポートします|



### メッセージ機能

| 機能タイプ | 機能の説明           |
| -------- | -------- |
| メッセージのダウンロード | App管理者は、このインターフェースを介して、App内の過去7日間のすべてのシングルまたはグループメッセージ記録を取得できます |
| オフラインメッセージ | ユーザーはログインしてからバックグラウンドに戻り、ユーザーがメッセージを送信すると、IMはオフラインプッシュをサポートします |
| ローミングメッセージ | 新しいデバイスにログインするとき、サーバー（クラウド）が記録した履歴メッセージのStorageを同期します。これはデフォルトで7日間保存され、有料で延長できます |
| マルチ端末同期 | マルチ端末メッセージの同期で、メッセージを同時に受信できます                               |
| 履歴メッセージ | ローカル履歴メッセージとクラウド履歴メッセージをサポートします                               |
| メッセージの取り消し | 配信に成功したメッセージを取り消すと、デフォルトで2分以内にメッセージが取り消されます。取り消し操作は、シングルチャットおよびグループチャットメッセージのみでサポートしており、ライブストリーミンググループ(AVChatRoom)の取り消しはサポートしていません |
| 開封確認 | ピアツーピアセッションで相手の既読・未読のステータスを確認します                           |
| メッセージ転送 | 他のユーザーまたはグループへメッセージを転送します                                   |
| @機能    | グループ内の@メッセージと通常のメッセージに本質的な違いはありませんが、@の付いた人がメッセージを受信すると、UIで特殊な処理を行う必要があります |
| 入力中 | オンラインメッセージを介して実現できます                                         |
| オフラインプッシュ | Apple APN、Xiaomiプッシュ、Huaweiプッシュ、Meizuプッシュ、OPPOプッシュ、vivoプッシュ、GoogleFCMプッシュをサポートします |
| メッセージの削除 | メッセージのremove方法を使用すると、メッセージをローカルで削除することができます                   |
| Red Packet機能 | Red Packetメッセージは@メッセージに類似しており、TIMCustomElemを介して実現できます          |
|全メンバープッシュ|IM通信アーキテクチャに基づいて実現するREST APIのセットで、Appアプリケーションの全メンバープッシュ、タグプッシュ、属性プッシュなどのメッセージプッシュ要件のサポートに用います。クライアントはSDKオンラインプッシュ、オフラインプッシュ（Androidバックグラウンド通知およびAPNs）を介してプッシュメッセージを受信できます|
|ローカルメッセージ検索|フレンドの検索、グループやグループメンバーの検索、メッセージの検索、セッションによるグループ化をサポートします|


### プロファイル機能

| 機能タイプ           | 機能の説明       |
| ------------------ | ---------------- |
| ユーザープロファイルの設定   | ユーザーが自分のニックネーム、検証方法、プロフィール画像、性別、年齢、署名、場所などのプロファイルを設定します |
| ユーザープロファイルの取得  | ユーザーが自分やフレンド、知らない人に関するプロファイルを確認します    |
| フィールドごとのユーザープロファイルの取得 | 特定のフィールドごとにユーザープロファイルを取得します       |
| カスタムユーザープロファイル     | 最大20件のカスタムユーザープロファイルフィールド      |



### リレーションシップチェーン機能

| 機能タイプ             | 機能の説明                  |
| -------------------- | ---------------------- |
| フレンドを探す             | ユーザーアカウントIDでフレンドを探すことができます           |
| フレンドの追加申請         | デフォルトで申請理由が必要かどうかを選択します。現在、デフォルトでは必要ありません       |
| フレンドの追加             | フレンド追加のリクエストを送信します            |
|フレンドのインポート|単方向のフレンドの一括インポートをサポートします|
|フレンドの更新|同じユーザーの複数のフレンドのリレーションシップチェーンデータの一括更新をサポートします|
| フレンドの削除             | フレンドにした後にフレンドを削除することができます         |
| すべてのフレンドの取得         | すべてのフレンドの取得は、デフォルトでは基本プロファイルのみを取得します       |
| フレンドを同意/拒否        | システムからフレンド追加のリクエスト通知を受け取った後、それを承認または拒否することができます   |
| ユーザーをブラックリストに追加     | 任意のユーザーをブラックリストに追加します。過去にフレンドだった場合はフレンドシップが解除されます    |
| ブラックリストから除外           | ブラックリストからユーザーを除外します              |
| ブラックリストの取得       | ユーザーのブラックリストを取得します                         |
| フレンドノート             | フレンドになると、 フレンドノートを送ることができます                |
| フレンドカスタムプロファイルの設定   | 最大20件のフレンドカスタムフィールドです              |
| フレンドグループの作成         | グループを作成するときに、追加するユーザーを同時に指定したり、同じユーザーを複数のグループに追加したりできます |
| フレンドグループの削除         | フレンドグループを削除します                       |
|フレンドのチェック|フレンドシップの一括チェックをサポートします|
|ブラックリストのチェック|ブラックリストの一括チェックをサポートします|
| フレンドを特定グループに追加     | フレンドをグループに追加します                |
| 特定グループからフレンドを削除     | グループからフレンドを削除します              |
| フレンドグループのリネーム       | フレンドグループをリネームします                      |
| 指定されたフレンドグループ情報の取得 | 指定されたフレンドグループを取得します                   |
| すべてのフレンドグループの取得     | すべてのグループ情報を取得します。また、すべてのフレンドを取得することで、グループ情報を取得することもできます |
| リレーションシップチェーンデータストレージ       | SDKはリレーションシップチェーンデータをストレージできます           |
| フレンドプロファイル変更のシステム通知 | フレンドプロファイルの変更時には、システムから通知を受信します               |
| リレーションシップチェーン変更のシステム通知 | リレーションシップチェーンの変更時にシステムから通知を受信できます               |



### グループ機能
IMは一般的なユースケースにもとづき、デフォルトで次のグループタイプを設定しています。
| 友だちワークグループ(Work)：作成後はすでにグループ内にいるフレンドのみを招待して参加させることができ、かつ被招待者側の同意またはグループマスターの承認は不要です。
- 知らない人とのソーシャルグループ(Public)：作成後はグループマスターがグループ管理者を指定できます。ユーザーはグループIDを検索してグループ参加申請を送信した後、グループマスターまたは管理者が申請を承認してからでないとグループに参加できません。
- 臨時ミーティンググループ(Meeting)：作成後は自由に参加・退出でき、かつグループ参加前のメッセージを確認する機能をサポートしています。音声/ビデオ会議のシナリオ、eラーニングのシナリオなどのTRTC製品と連携させたシナリオに適しています。
- ライブストリーミンググループ(AVChatRoom)：作成後は自由に参加・退出ができ、グループ参加者数の上限はありませんが、メッセージ履歴の保存はサポートしていません。CSS製品との連携に適しており、弾幕チャットのシナリオに使用します。

各グループタイプのデフォルトの機能の違いは、次のとおりです。

<table>
   <tr>
      <th width="0px" style="text-align:center">機能タイプ</td>
      <th width="0px" style="text-align:center">友だちワークグループ（Work）</td>
			 <th width="0px" style="text-align:center">知らない人とのソーシャルグループ（Public）</td>
       <th width="0px" style="text-align:center">臨時ミーティンググループ（Meeting）</td>
			 <th width="0px" style="text-align:center">ライブストリーミンググループ(AVChatRoom)</td>
   </tr>
   <tr>
      <td style="text-align:center">メンバー上限</td>
      <td ><li>体験版：20人/グループ</li><br><li>プロフェッショナル版：デフォルトは200人/グループで、付加価値機能により最大2,000人/グループまでの拡張をサポートします</li><br><li>フラッグシップ版：デフォルトは2,000人/グループで、付加価値機能により最大6,000人/グループまでの拡張をサポートします</li></td>
			      <td><li>体験版：20人/グループ</li><br><li>プロフェッショナル版：デフォルトは200人/グループで、付加価値機能により最大2,000人/グループまでの拡張をサポートします</li><br><li>フラッグシップ版：デフォルトは2,000人/グループで、付加価値機能により最大6,000人/グループまでの拡張をサポートします</li></td>
						      <td ><li>体験版：20人/グループ</li><br><li>プロフェッショナル版：デフォルトは200人/グループで、付加価値機能により最大2,000人/グループまでの拡張をサポートします</li><br><li>フラッグシップ版：デフォルトは2,000人/グループで、付加価値機能により最大6,000人/グループまでの拡張をサポートします</li></td>
									      <td>上限なし</td>
   </tr>
   <tr>
     <td>グループプロファイルの変更</td>
     <td>グループメンバー</td>
    <td><li>グループ管理者</li><br><li>グループマスター</li><br><li>App管理者</li></td>
    <td><li>グループマスター</li><br><li>App管理者</li></td>
    <td>App管理者</td>
   </tr>
	   <tr>
     <td>メンバーリスト</td>
     <td>すべて表示</td>
    <td>すべて表示</td>
    <td>すべて表示</td>
    <td>300人を表示</td>
   </tr>
	   <tr>
     <td>グループの解散</td>
     <td>App管理者</td>
    <td><li>グループマスター</li><br><li>App管理者</li></td>
    <td><li>グループマスター</li><br><li>App管理者</li></td>
    <td><li>グループマスター</li><br><li>App管理者</li></td>
   </tr>
	   <tr>
     <td>グループ参加の申請</td>
     <td>サポートしていません</td>
    <td>許可</td>
    <td>許可</td>
    <td>許可</td>
   </tr>
	   <tr>
     <td>グループ参加の承認</td>
     <td>サポートしていません</td>
    <td>要承認</td>
    <td>承認なし</td>
    <td>承認なし</td>
   </tr>
	   <tr>
     <td>グループ参加の招待</td>
     <td>被招待者は承認不要</td>
    <td>サポートしていません</td>
    <td>サポートしていません</td>
    <td>サポートしていません</td>
   </tr>
	 	   <tr>
     <td>グループマスターがグループから退出</td>
     <td>サポートしています</td>
    <td>未サポート</td>
    <td>サポートしていません</td>
    <td>サポートしていません</td>
   </tr>
	 	   <tr>
     <td>管理者の設定</td>
     <td>サポートしていません</td>
    <td>サポートしています</td>
    <td>サポートしています</td>
    <td>サポートしていません</td>
   </tr>
		 	   <tr>
     <td>メンバーの退出</td>
    <td><li>グループマスター</li><br><li>App管理者</li></td>
    <td><li>グループ管理者</li><br><li>グループマスター</li><br><li>App管理者</li></td>
    <td><li>グループ管理者</li><br><li>グループマスター</li><br><li>App管理者</li></td>
    <td>サポートしていません</td>
   </tr>
		 	   <tr>
     <td>グループ参加前の履歴メッセージの表示をサポートしていますか</td>
     <td>サポートしていません</td>
    <td>サポートしていません</td>
    <td>サポートしています</td>
    <td>サポートしていません</td>
   </tr>
		 	   <tr>
     <td>メンバー変更通知</td>
     <td>全メンバー</td>
    <td>全メンバー</td>
    <td>なし</td>
    <td>全メンバー</td>
   </tr>
		 	   <tr>
     <td>グループアクティベーション</td>
     <td>メッセージアクティベーション</td>
    <td>不要</td>
    <td>不要</td>
    <td>不要</td>
   </tr>
	 	   <tr>
     <td>メンバーミュート</td>
     <td>サポートしていません</td>
    <td>サポートしています</td>
    <td>サポートしています</td>
    <td>サポートしています</td>
   </tr>
		 	   <tr>
     <td>未読数カウント</td>
     <td>サポートしています</td>
    <td>サポートしています</td>
    <td>サポートしています</td>
    <td>サポートしていません</td>
   </tr>
		 	   <tr>
     <td>ゲストとしてメッセージを受信</td>
     <td>サポートしていません</td>
    <td>サポートしていません</td>
    <td>サポートしていません</td>
    <td>サポートしています</td>
   </tr>
		 	   <tr>
     <td>メッセージ履歴の保存</td>
     <td>サポートしています</td>
    <td>サポートしています</td>
    <td>サポートしています</td>
    <td>サポートしていません</td>
   </tr>
		 	   <tr>
     <td>デフォルトのメッセージ受信オプション</td>
     <td>オンラインプッシュメッセージとオフラインプッシュの受信</td>
    <td>オンラインプッシュメッセージとオフラインプッシュの受信</td>
    <td>オンラインプッシュメッセージのみを受信</td>
    <td>オンラインプッシュメッセージのみを受信</td>
   </tr>
		 	   <tr>
     <td>グループのインポート</td>
     <td>サポートしています</td>
    <td>サポートしています</td>
    <td>サポートしています</td>
    <td>サポートしていません</td>
   </tr>
</table>




### IMコンソール

Tencent Cloud[IMコンソール](https://console.cloud.tencent.com/im)で、必要に応じてアプリケーションを設定できます。

| 機能タイプ    | 機能の説明                  |
| ------- | --------------------- |
| アプリケーションの作成    | アプリケーションを新規作成します                  |
| アプリケーションのアップグレード    | パッケージバージョンをアップグレードします               |
| SDKのダウンロード  | クライアントのSDKをダウンロードします            |
| アプリケーション設定    | アプリケーションを設定できます               |
| 統計分析    | 運用データを確認します                |
| コールバック設定    | サードパーティのコールバック                 |
| 機能設定    | カスタムフィールドとオンラインインスタンスを追加します          |
| グループ管理    | グループの追加、変更、解散、グループメンバーの管理、メッセージの送信を行います |
| 開発者支援ツール | Web上でUserSigを発行します        |
| セキュリティ対策    | 不適切なメッセージを識別して取り締まります          |



### データ統計

IMコンソールの[統計分析](https://console.cloud.tencent.com/im)機能には、さまざまな次元のデータ統計があり、お客様に運用データを提供します。

| 統計タイプ     | 機能の説明              |
| -------- | ----------------- |
| アクティブユーザー数    | サーバーと接続しインタラクションしている重複を除去したユーザー数  |
| 新規登録ユーザー数  | 新規登録ID数        |
| 登録ユーザー累計数  | すべての登録ユーザー数を確認します         |
| アップストリームメッセージ数    | アップストリームメッセージ数を確認する時間を選択できます     |
| メッセージ送信人数   | メッセージ送信人数を確認する時間を選択できます    |
| 同時オンライン最大人数 | 同時オンライン人数を確認する時間を選択できます  |
| シングルチャットアップストリームメッセージ数    | シングルチャットアップストリームメッセージ数を確認する時間を選択できます     |
| シングルチャットのメッセージ送信人数  | シングルチャットのメッセージ送信人数を確認する時間を選択できます   |
| グループチャットアップストリームメッセージ数    | グループチャットアップストリームメッセージ数を確認する時間を選択できます     |
| グループチャットのメッセージ送信人数  | グループチャットのメッセージ送信人数を確認する時間を選択できます   |
| メッセージ送信グループ数   | メッセージ送信グループ数を確認する時間を選択できます    |
| 追加グループ数   | 追加グループ数を確認する時間を選択できます    |
| 累計グループ数    | 累計グループ数を確認する時間を選択できます     |
| データのエクスポート     | データをエクスポートする時間を選択できます       |

### リアルタイムモニタリング
IMコンソールの[統計分析](https://console.cloud.tencent.com/im)機能には、さまざまな次元のデータ統計があり、お客様に運用データを提供します。

| 統計タイプ     | 機能の説明       |
| -------- | ---------- |
| 現在のオンラインユーザー数  | リアルタイムのオンラインユーザー数     |
| 本日のシングルチャットメッセージ量  | その日のシングルチャットメッセージの総量   |
| 本日の一般的なグループメッセージ量 | その日の非ライブストリーミンググループメッセージの総量 |
| 本日のライブストリーミンググループメッセージ量 | その日のライブストリーミンググループメッセージの総量 |

### 民営化サポート
プライベートデプロイにより、企業はシステムを自社のサーバーに直接デプロイすることができ、データはローカルにそのまま保存されます。IMは、プライベートデプロイ機能をサポートしており、企業によるプライベートバージョンのデプロイ・実施・運用・保守を支援することができます。利用する必要がある場合は、 [IMプライベートサービス](https://intl.cloud.tencent.com/apply/p/itvi76h023)で申請してください。
>?申請するときは、Tencent Cloudルートアカウントにログインする必要があります。
