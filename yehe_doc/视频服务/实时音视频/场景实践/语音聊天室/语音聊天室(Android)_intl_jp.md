## デモンストレーション
[ダウンロード](https://intl.cloud.tencent.com/document/product/647/35076)からAppをインストールして、マイク管理、低レイテンシー音声インタラクション、文字チャットなどのボイスチャットのユースケースにおけるTRTCの関連機能を含む、ボイスチャットルームの機能を体験できます。


ボイスチャットルーム機能をすばやく実装する必要がある場合は、当社が提供するAppを基に直接変更を加えて適合させることも、当社が提供するTRTCVoiceRoomコンポーネントでカスタマイズしたUIを実装することも可能です。

[](id:DemoUI)
## AppのUIの再利用

[](id:ui.step1)
### 手順1：アプリケーションの新規作成
1．TRTCコンソールにログインし、【開発支援】>【[Demoクイックスタート](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2. `TestLiveRoom`などのアプリケーション名を入力して、【作成】をクリックします。
3. 【ダウンロードしました。次のステップ】をクリックすると、この手順をスキップします。

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)
>!本機能はTencent Cloudの[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://intl.cloud.tencent.com/document/product/1047)という2つの基本的なPaaSサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期的にアクティブにすることができます。IMは付加価値サービスであり、課金ルールの詳細については、[Instant Messagingの料金説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。



[](id:ui.step2)
### 手順2：Appソースコードのダウンロード
クリックして[TUIVoiceRoom](https://github.com/tencentyun/TUIVoiceRoom)に進み、ソースコードをCloneまたはダウンロードします。

[](id:ui.step3)
### 手順3：Appプロジェクトファイルの設定
1. 設定変更ページに進み、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2. `Android/Debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java`のファイルを見つけて開きます。
3. `GenerateTestUserSig.java`ファイル内の関連パラメータを設定します。
<ul style="margin:0"><li/>SDKAPPID：デフォルトはプレースホルダー(PLACEHOLDER)。実際のSDKAppIDを設定してください。
<li/>SECRETKEY：デフォルトはプレースホルダー(PLACEHOLDER)。実際のキー情報を設定してください。</ul>

4. 貼り付け完了後、【貼り付けました。次のステップ】をクリックすれば、作成が完了します。
5. コンパイル完了後、【コンソール概要に戻る】をクリックすればOKです。


>!
>- ここで言及するUserSigの発行方法は、クライアントコードの中でのSECRETKEY設定となりますが、この手法のSECRETKEYは逆コンパイルによって逆クラッキングされやすく、キーがいったん漏洩すると、攻撃者がお客様のTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのAppクイックスタートおよび機能デバッグにのみ適しています**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。UserSigが必要なときは、Appから業務サーバーにリクエストを送信し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

[](id:ui.step4)
### 手順4：Appの実行
Android Studio（バージョン3.5以上）を使用してソースコード`TUIVoiceRoom`プロジェクトを開き、【実行】をクリックすれば、このAppのデバッグが開始されます。

[](id:ui.step5)
### 手順5：Appソースコードの修正
ソースコードのSourceフォルダは、uiとmodelという2つのサブフォルダを含んでいます。uiフォルダにはインターフェースコードが含まれています。以下の表にファイルまたはフォルダおよび対応するUIをリストアップして、二次調整を行いやすくしています。

| ファイルまたはフォルダ | 機能の説明 |
|-------|--------|
| base | UIに使用される基礎となるクラス。 |
| room | メインルームページは、管理者とリスナーという2種類のインターフェースがあります。 |
| widget | 汎用ウィジェット。 |

## 体験アプリケーション
>! 体験アプリケーションには、少なくとも2台のデバイスが必要です。

### ユーザーA
1. 図のように、ユーザー名を入力し（**ユーザー名は一意のものとし、他のユーザーと重複しないようにしてください**）、ログインします。
2. 下図のように、【ルームの作成】をクリックします。
3. ルームトピックを入力し、【チャット開始】をクリックします。

### ユーザーB
1. 図のように、ユーザー名を入力し（**ユーザー名は一意のものとし、他のユーザーと重複しないようにしてください**）、ログインします。
2. ユーザーAが作成したルーム番号を入力し、【入室する】をクリックします。<br>

>!  ルーム番号はユーザーAのルーム上部に表示されます。

[](id:model)

## カスタマイズUIの実装

[ソースコード](https://github.com/tencentyun/TUIVoiceRoom/tree/main/Android/Source/src/main/java/com/tencent/liteav/trtcvoiceroom)のSourceフォルダには、uiとmodelという2つのサブフォルダがあり、modelフォルダには再利用できるオープンソースコンポーネントTRTCVoiceRoomがあります。`TRTCVoiceRoom.java`ファイルでこのコンポーネントが提供するインターフェース関数を確認し、対応するインターフェースを使用してカスタマイズしたUIを実装することができます。
![](https://main.qcloudimg.com/raw/319beb14d72a43120e102380278aa1da.png)

[](id:model.step1)
### 手順1：SDKへの統合
ボイスチャットコンポーネントTRTCVoiceRoomは、TRTC SDKとIM SDKに依存し、次の手順で2つのSDKをプロジェクトに統合することができます。

**方法1：Mavenリポジトリを介する依存**
1. dependenciesにTRTCSDKとIMSDKの依存を追加します。
<dx-codeblock>
::: java java
dependencies {
       complie "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
       complie 'com.tencent.imsdk:imsdk:latest.release'
       compile 'com.google.code.gson:gson:2.3.1'
}
:::
</dx-codeblock>
>?2つのSDKの最新バージョン番号は、[TRTC](https://github.com/tencentyun/TRTCSDK)および[IM](https://github.com/tencentyun/TIMSDK)のGitHubトップページで取得することができます。
2. defaultConfigでAppが使用するCPUアーキテクチャを指定します。
<dx-codeblock>
::: java java
defaultConfig {
      ndk {
          abiFilters "armeabi-v7a"
      }
}
:::
</dx-codeblock>
3. 【Sync Now】をクリックし、自動でSDKをダウンロードし、プロジェクトに統合します。

**方法2：ローカルAARを介する依存**
開発環境でのMavenリポジトリへのアクセスが遅い場合は、ZIPパッケージを直接ダウンロードし、統合ドキュメントに従って手動でプロジェクトに統合することができます。
<table>
<tr>
<th>SDK</th>
<th>ダウンロードページ</th>
<th>統合ガイド</th>
</tr>
<tr>
<td>TRTC SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/35093">統合ドキュメント</a></td>
</tr>
<tr>
<td>IM SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34306">統合ドキュメント</a></td>
</tr>
</table>

[](id:model.step2)
### 手順2：権限の設定および難読化ルール
AndroidManifest.xmlにAppの権限を設定します。SDKには次の権限が必要です（6.0以降のAndroidシステムではストレージ読み取りの権限を動的に申請する必要があります）。
<dx-codeblock>
::: java java
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
:::
</dx-codeblock>

proguard-rules.proファイルでは、SDK関連クラスを非難読化リストに追加します。
<dx-codeblock>
::: java java
-keep class com.tencent.** { *; }
:::
</dx-codeblock>

[](id:model.step3)
### 手順3：TRTCVoiceRoomコンポーネントをインポート
次のディレクトリ内のすべてのファイルをプロジェクトにコピーします。
<dx-codeblock>
::: java java
Source/src/main/java/com/tencent/liteav/trtcvoiceroom/model
:::
</dx-codeblock>

[](id:model.step4)
### 手順4：コンポーネントの作成およびログイン
1. `sharedInstance` インターフェースを呼び出すと、TRTCVoiceRoomコンポーネントのインスタンスオブジェクトを作成できます。
2. `setDelegate`関数を呼び出してコンポーネントのイベント通知を登録します。
3. `login`関数を呼び出してコンポーネントのログインを完了します。下表を参考にキーパラメータを入力してください。
 <table>
<tr>
<th>パラメータ名</th>
<th>作用</th>
</tr>
<tr>
<td>sdkAppId</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTCコンソール</a> でSDKAppIDを表示できます。</td>
</tr>
<tr>
<td>userId</td>
<td>現在のユーザーID。文字列タイプでは、英語のアルファベット（a-zとA-Z）、数字（0-9）、ハイフン（-）とアンダーライン（_）のみ使用できます。</td>
</tr>
<tr>
<td>userSig</td>
<td>Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については、<a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSigの計算方法</a>をご参照ください。</td>
</tr>
<tr>
<td>callback</td>
<td>ログインのコールバック。成功時にcodeは0になります。</td>
</tr>
</table>
<dx-codeblock>
::: java java
TRTCVoiceRoom mTRTCVoiceRoom = TRTCVoiceRoom.sharedInstance(this);
mTRTCVoiceRoom.setDelegate(this);
mTRTCVoiceRoom.login(SDKAPPID, userId, userSig, new TRTCVoiceRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {![](https://main.qcloudimg.com/raw/3151fc0df16c063db7a75f6c1facf562.png)
            //ログイン成功
        }
    }
});
:::
</dx-codeblock>

[](id:model.step5)
### 手順5：管理者側での配信開始
1. 管理者は、[手順4](#model.step4)でログイン後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. 管理者は、`createRoom`を呼び出して新しいボイスチャットルームを作成します。この時にルームID、マイク・オンに管理者の確認の要否、マイク数などルームのプロパティ情報を渡します。
3. 管理者は、ルーム作成に成功した後、`enterSeat`を呼び出して参加します。
4. 管理者は、コンポーネントの`onSeatListChange`マイクリスト変更イベント通知を受信します。この時、マイクリストの変更をUI上に更新することができます。
5. 管理者は、マイクリストのメンバーが参加した`onAnchorEnterSeat`というイベント通知も受信します。この時、マイク集音は自動的に開始されます。

![](https://main.qcloudimg.com/raw/256ebe5ce1426b3f175c8c8b68095d5b.png)


<dx-codeblock>
::: java java
// 1.管理者は、ニックネームおよびプロフィール画像を設定します
mTRTCVoiceRoom.setSelfProfile("my_name", "my_face_url", null);

// 2.管理者は、createRoomを呼び出してルームを作成します
final TRTCVoiceRoomDef.RoomParam roomParam = new TRTCVoiceRoomDef.RoomParam();
roomParam.roomName = "ルーム名";
roomParam.needRequest = false; // マイク・オンの管理者による確認の要否
roomParam.seatCount = 7; // ルームの座席数。ここでは計7席あり、管理者が1席を占め、残り6席がリスナーとなります
roomParam.coverUrl = 「ルームカバー図のURL」;
mTRTCVoiceRoom.createRoom(mRoomId, roomParam, new TRTCVoiceRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            //3. 0番の席を占有します
            mTRTCVoiceRoom.enterSeat(0, new TRTCVoiceRoomCallback.ActionCallback() {
                @Override
                public void onCallback(int code, String msg) {
                    if (code == 0) {
                    }
                }
            });
        }
    }
});

// 4.席の占有に成功した後、onSeatListChangeイベント通知を受信します
@Override
public void onSeatListChange(final List<TRTCVoiceRoomDef.SeatInfo> seatInfoList) {
    // マイクリストの表示
}

// 5.  onAnchorEnterSeatイベント通知を受信
@Override
public void onAnchorEnterSeat(TRTCVoiceRoomDef.UserInfo userInfo) {
}
:::
</dx-codeblock>

[](id:model.step6)
### 手順6：リスナー側の視聴
1. リスナー側は、[手順4](#model.step4)でログイン後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. リスナー側は、業務バックエンドに最新のボイスチャットルームのルームリストを取得します。
>?Appのボイスチャットルームリストは、デモンストレーション用のためだけのものです。ボイスチャットルームリストのビジネスロジックは様々です。Tencent Cloudは現在、ボイスチャットルームリストの管理サービスを提供していませんので、ご自身でボイスチャットのルームリストを管理してください。
3. リスナー側は、`getRoomInfoList`を呼び出してルームの詳細情報を取得します。この情報は、管理者側が`createRoom`を呼び出してボイスチャットルームを作成するときに設定する簡単な説明情報です。
>!ボイスチャットルームのリストに十分に包括的な情報がある場合は、 `getRoomInfoList` の呼び出しに関する手順をスキップできます。
4．リスナーは1つのボイスチャットルームを選択し、`enterRoom`を呼び出してルームナンバーを渡すと、そのルームに参加できます。
5. 入室後、コンポーネントの`onRoomInfoChange` ルーム属性変更イベント通知を受信します。この時、ルーム属性を記録し、それに応じた修正を行うことができます。例：UIに表示するルーム名、発言者にする際の管理者への同意リクエストの要否の記録など。
6. 入室後は、コンポーネントの`onSeatListChange`マイクリスト変更イベント通知を受信します。この時、マイクリストの変更をUI上に更新することができます。
7. 入室後、マイクリストにキャスターが参加した `onAnchorEnterSeat` のイベント通知も受信します。

![](https://main.qcloudimg.com/raw/33432f97eb632fbb9710a59cba9e4469.png)
<dx-codeblock>
::: java java
// 1.リスナーは、ニックネームおよびプロフィール画像を設定します
mTRTCVoiceRoom.setSelfProfile("my_name", "my_face_url", null);

// 2.業務バックエンドから取得したルームリストをroomListと仮定します
List<Integer> roomList = GetRoomList();

// 3.getRoomInfoListを呼び出すことによって、ルームの詳細情報を取得します
mTRTCVoiceRoom.getRoomInfoList(roomList, new TRTCVoiceRoomCallback.RoomInfoCallback() {
    @Override
    public void onCallback(int code, String msg, List<TRTCVoiceRoomDef.RoomInfo> list) {
        if (code == 0) {
            // この時、自分のUIルームリストを更新することができます
        }
    }
});

// 4.ボイスチャットルームを選択後、roomIdを渡して入室します
mTRTCVoiceRoom.enterRoom(roomId, new TRTCVoiceRoomCallback.ActionCallback() {
        @Override
        public void onCallback(int code, String msg) {
            if (code == 0) {
                //入室に成功
            }
        }
});

// 5.入室に成功後、onRoomInfoChangeイベント通知を受信します
@Override
public void onRoomInfoChange(TRTCVoiceRoomDef.RoomInfo roomInfo) {
    mNeedRequest = roomInfo.needRequest;
    mRoomName = roomInfo.roomName;
    // UIはタイトルなどを表示することができます
}

// 6.入室に成功後、onSeatListChangeイベント通知を受信します
@Override
public void onSeatListChange(final List<TRTCVoiceRoomDef.SeatInfo> seatInfoList) {
    // マイクリストの表示
}

// 7. onAnchorEnterSeatイベント通知を受信します
@Override
public void onAnchorEnterSeat(TRTCVoiceRoomDef.UserInfo userInfo) {
}
:::
</dx-codeblock>

[](id:model.step7)
### 手順7：マイク管理

<dx-tabs>
::: 管理者側
1. `pickSeat`は、対象となるマイクおよびリスナーのuserIdを渡し、発言できるように視聴者を招待できます。ルーム内の全メンバーは`onSeatListChange`および`onAnchorEnterSeat`というイベント通知を受信します。
2. `kickSeat`は、対象となるマイクを渡した後、キックアウトしてマイク・オフにすることができます。ルーム内の全メンバーは`onSeatListChange`および`onAnchorLeaveSeat`というイベント通知を受信します。
3. `muteSeat`は、対象となるマイクを渡した後、ミュート/ミュート解除をすることができます。ルーム内の全メンバーは`onSeatListChange`および`onSeatMute`というイベント通知を受信します。
4．`closeSeat`は、対応するマイクを送信後、任意のマイクのクローズ/解除をすることができます。クローズ後は、リスナー側はこれ以上マイクを使用することはできません。ルーム内の全参加者は`onSeatListChange`および`onSeatClose`というイベント通知を受信します。
![](https://main.qcloudimg.com/raw/367a0c670d2f9899d0b311ed1f322ea3.png)

:::
::: リスナー側
1. `enterSeat`は、対象となるマイクを渡した後、マイク・オンにすることができます。ルーム内の全メンバーは`onSeatListChange`および`onAnchorEnterSeat`というイベント通知を受信します。
2. `leaveSeat`でユーザーが視聴者になります。ルーム内の全メンバーは`onSeatListChange`および`onAnchorLeaveSeat`というイベント通知を受信します。

![](https://main.qcloudimg.com/raw/8d385dd387b6255b8512dbff5829e88a.png)

マイク操作後のイベント通知の順番は次のとおりです。callback > onSeatListChange > onAnchorEnterSeatなど独立したイベント。

<dx-codeblock>
::: java java
// 1: 管理者がピックして1号マイクをマイク・オンにします
mTRTCVoiceRoom.pickSeat(1, "123", new TRTCVoiceRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        // 2. callbackコールバックを受信します
        if (code == 0) {
        }
    }
});

// 3. onSeatListChangeコールバックを受信し、マイクリストを更新します
@Override
public void onSeatListChange(final List<TRTCVoiceRoomDef.SeatInfo> seatInfoList) {
}

// 4.単一のマイク変更の通知によって、ここでリスナーが実際にマイク・オンに成功したかを判断することができます
public void onAnchorEnterSeat(int index, TRTCVoiceRoomDef.UserInfo user) {
}
:::
</dx-codeblock>

<dx-codeblock>
::: java java
// 1: リスナーが自主的に2号マイクをマイク・オンにします
mTRTCVoiceRoom.enterSeat(2, new TRTCVoiceRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        // 2. callbackコールバックを受信します
        if (code == 0) {
        }
    }
});

// 3. onSeatListChangeコールバックを受信し、マイクリストを更新します
@Override
public void onSeatListChange(final List<TRTCVoiceRoomDef.SeatInfo> seatInfoList) {
}

// 4.単一のマイク変更の通知によって、ここでご自身が適切な処理を行っているか判断することができます
public void onAnchorEnterSeat(int index, TRTCVoiceRoomDef.UserInfo user) {
}
:::
</dx-codeblock>
:::
</dx-tabs>


[](id:model.step8)
### 手順8：招待シグナリングの使用
[マイク管理](#model.step7)では、リスナーがマイク・オン/オフにする場合や、管理者が視聴者を発言できるように招待する場合は、相手の同意を必要とせずに直接操作することができます。
Appが次の操作の業務フローを実施するために、相手の同意を必要とする場合、招待シグナリングによって対応するサポートを提供することができます。

<dx-tabs>
::: リスナーからの自主的なマイク・オン申請
1. リスナー側が`sendInvitation`を呼び出し、管理者のuserIdおよび業務のカスタムコマンドワードなどを渡します。この時、関数が1つのinviteIdを返しますので、このinviteIdを記録します。
2. 管理者側は、`onReceiveNewInvitation`というイベント通知を受信します。この時UIでウィンドウをポップアップさせ、管理者に同意の有無をたずねることができます。
3. 管理者が同意を選択後、`acceptInvitation`を呼び出してinviteIdを渡します。
4. リスナー側は、`onInviteeAccepted`というイベント通知を受信し、`enterSeat`を呼び出してマイク・オンにします。

![](https://main.qcloudimg.com/raw/5ccdb15f63efa127aa883ca6a7bcd80d.png)

<dx-codeblock>
::: java java
// リスナー側の視点
// 1. sendInvitationを呼び出し、1号マイクの使用をリクエストします
String inviteId = mTRTCVoiceRoom.sendInvitation("ENTER_SEAT", ownerUserId, "1", null);

// 2.招待のリクエスト同意を受信し、正式にマイク・オンになります
@Override
public void onInviteeAccepted(String id, String invitee) {
    if(id.equals(inviteId)) {
        mTRTCVoiceRoom.enterSeat(1, null);
    }
}

// 管理者側の視点
// 1.管理者がリクエストを受信します
 @Override
public void onReceiveNewInvitation(final String id, String inviter, String cmd, final String content) {
    if (cmd.equals("ENTER_SEAT")) {
        // 2.管理者がリスナーのリクエストに同意します
         mTRTCVoiceRoom.acceptInvitation(id, null);
    }
}
:::
</dx-codeblock>
:::
::: 管理者からの招待によるリスナーのマイク・オン
1. 管理者側が`sendInvitation`を呼び出し、リスナーのuserIdおよび業務のカスタムコマンドワードなどを渡します。この時、関数が1つのinviteIdを返しますので、このinviteIdを記録します。
2. リスナー側は、`onReceiveNewInvitation`というイベント通知を受信します。この時UIでウィンドウをポップアップさせ、リスナーに同意の有無をたずねることができます。
3. リスナーが同意を選択後、`acceptInvitation`を呼び出してinviteIdを渡します。
4. 管理者側は、`onInviteeAccepted`というイベント通知を受信し、`pickSeat`を呼び出して、リスナーをピックしてマイク・オンにします。

![](https://main.qcloudimg.com/raw/5515f49d6e30410e12cd828b75a8db0b.png)

<dx-codeblock>
::: java java
// 管理者側の視点
// 1.管理者はsendInvitationを呼び出して、リスナー「123」をピックして2号マイクのマイク・オンをリクエストします
String inviteId = mTRTCVoiceRoom.sendInvitation("PICK_SEAT", "123", "2", null);

// 2.招待のリクエスト同意を受信し、正式にマイク・オンになります
@Override
public void onInviteeAccepted(String id, String invitee) {
    if(id.equals(inviteId)) {
        mTRTCVoiceRoom.pickSeat(2, null);
    }
}

// リスナー側の視点
// 1.リスナーがリクエストを受信します
 @Override
public void onReceiveNewInvitation(final String id, String inviter, String cmd, final String content) {
    if (cmd.equals("PICK_SEAT")) {
        // 2.リスナーが管理者のリクエストに同意します
         mTRTCVoiceRoom.acceptInvitation(id, null);
    }
}
:::
</dx-codeblock>
:::
</dx-tabs>


[](id:model.step9)
### 手順9：文字チャットおよび弾幕コメントの実装
- `sendRoomTextMsg`によって通常のテキストメッセージを送信できるようになり、このルーム内のすべてのキャスターおよびリスナーが`onRecvRoomTextMsg`のコールバックを受信することができます。
 IMバックエンドは、デフォルトのセンシティブワードフィルタルールを備えており、センシティブワードと認識されたテキストメッセージはクラウドに転送されることはありません。
  <dx-codeblock>
  ::: java java
  // 送信側：テキストメッセージの送信
  mTRTCVoiceRoom.sendRoomTextMsg("Hello Word!", null);
  // 受信側：テキストメッセージの監視
  mTRTCVoiceRoom.setDelegate(new TRTCVoiceRoomDelegate() {
    @Override
    public void onRecvRoomTextMsg(String message, TRTCVoiceRoomDef.UserInfo userInfo) {
        Log.d(TAG, userInfo.userName + "からのメッセージを受信:" + message);
    }
  });
  :::
  </dx-codeblock>
- `sendRoomCustomMsg`によって、カスタム（シグナル）メッセージを送信できます。当該ルーム内のすべてのキャスターとリスナーが`onRecvRoomCustomMsg`コールバックを受信できます。
カスタムメッセージは、カスタマイズ信号の送信によく用いられます。例えば、「いいね」情報の発信やブロードキャストに使用します。
<dx-codeblock>
::: java java
// 送信側：カスタマイズCmdによって弾幕と「いいね」情報を区別することができます
// eg:「CMD_DANMU」は弾幕コメントを表し、「CMD_LIKE」は「いいね」情報を表します
mTRTCVoiceRoom.sendRoomCustomMsg("CMD_DANMU", "Hello world", null);
mTRTCVoiceRoom.sendRoomCustomMsg("CMD_LIKE", "", null);
// 受信側：カスタムメッセージの監視
mTRTCVoiceRoom.setDelegate(new TRTCVoiceRoomDelegate() {
    @Override
    public void onRecvRoomCustomMsg(String cmd, String message, TRTCVoiceRoomDef.UserInfo userInfo) {
        if ("CMD_DANMU".equals(cmd)) {
            // 弾幕コメントの受信
            Log.d(TAG, "が" + userInfo.userName + "から受信した弾幕コメント:" + message);
        } else if ("CMD_LIKE".equals(cmd)) {
            // 「いいね」情報の受信
            Log.d(TAG、 userInfo.userName + 「いいねを付けました！」);
        }
    }
});
:::
</dx-codeblock>
