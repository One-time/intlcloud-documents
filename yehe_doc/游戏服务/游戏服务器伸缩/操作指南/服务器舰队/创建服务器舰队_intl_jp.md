## 操作シナリオ

ここでは、主にサーバーフリートの作成方法をご説明します。フリートは1組の CVMインスタンス形式のホスティングリソースを採用し、フリートのサイズはフリートのために指定したインスタンスの数によって決まります。また手動または自動でスケールアウトして、フリートのサイズを調整し、プレイヤーのニーズを満たすことができます。ホスティングのサーバーフリートはゲームサーバーのデプロイに使用します。



## 操作手順

1. [GSEコンソール](https://console.cloud.tencent.com/gse/asset)にログインし、左側メニューの【サーバーフリート】をクリックし、サーバーフリートページに入ります。
2. 左上のサービスエリアを選択し、【新規作成】をクリックします。
3. サーバーフリートの作成ページに入り、[基本情報](#.E5.9F.BA.E6.9C.AC.E4.BF.A1.E6.81.AF)、[プロセス管理](#.E8.BF.9B.E7.A8.8B.E7.AE.A1.E7.90.86)、[デプロイ設定](#.E9.83.A8.E7.BD.B2.E9.85.8D.E7.BD.AE)、[ネットワーク](#.E7.BD.91.E7.BB.9C)などの情報を入力します。

### 基本情報
サーバーフリートの作成は、リソースタイプに応じて「アセット」による作成と「イメージ」による作成の2種類に分かれます。具体的な説明は以下のとおりです。

- **アセットによる作成**
![](https://main.qcloudimg.com/raw/c47bfd7a581fa7152edfaec6c4ebd3c7.png)
  - 名称：サーバーフリート名を作成します。リストの中で簡単に識別できるように、意味をもつフリート名を作成することをお勧めします。
  - リソースタイプ：プルダウンリストからアセットを選択します。
  - アセット名：プルダウンリストから作成した有効なアセットを選択します。アセットがない場合は、先に[アセットを作成](https://intl.cloud.tencent.com/document/product/1055/36674)してください。
  - 説明：サーバーフリートの説明を作成し、さらに識別しやすくします（任意）。
  - アセットID、アセットのサイズ、OSは、選択したアセット名に基づき自動的に入力されます。

- **イメージによる作成**
![](https://main.qcloudimg.com/raw/8158e3185b3b42bbd01487d1926adf6b.png)
  - 名称：サーバーフリート名を作成します。リストの中で簡単に識別できるように、意味をもつフリート名を作成することをお勧めします。
  - リソースタイプ：プルダウンリストからイメージを選択します。
  - イメージリソース名：プルダウンリストから作成した有効なイメージリソースを選択します。イメージリソースがない場合は、先に[イメージを作成](https://intl.cloud.tencent.com/zh/document/product/1055/39061)してください。
  - 説明：サーバーフリートの説明を作成し、さらに識別しやすくします（任意）。
  - イメージID、イメージのサイズ、イメージのOSは、選択したイメージ名に基づき自動的に入力されます。
 >!フリートの「イメージによる作成」を選択した場合、イメージについての権限を与える必要もあります。フリート作成に使用するイメージリソースの権限をGSEに与える必要があり、【クリックして共有】>【Cloud Access Managementに進む】>【権限付与に同意】をクリックすると、イメージリソースが使用できるようになります。
>

### プロセス管理
  サーバープロセスが各CVMインスタンス上で動作する方式を設定します。
  - 起動パス：アセットの中のゲーム実行可能ファイルのパスを入力します。Linuxプラットフォームでは、アセットは`/local/game/`パスにダウンロードします。Windowsプラットフォームでは、アセットは`C:\game\`パスにダウンロードします。ゲームプロセス解凍後のフルパスは次のとおりです。
   - Liunx:`/local/game/YourGameServerBuild`
   - Windows:`C:\game\YourGameServerBuild.exe`
  - 起動パラメータ：起動時に情報をゲームの実行可能ファイルに転送することができ、コマンドラインパラメータ形式で情報をキー入力します（任意）。
  - 許容並列プロセス数：サーバーフリートの各CVMインスタンス上で、この設定を使用するサーバープロセスの並列実行数を指定します。
  - 最大並列起動ゲームサーバーセッション数： CVMインスタンス上で同時にアクティベート可能なゲームサーバーセッションの数を制限します。制限なし、制限あり（最大値：20000）を選択できます。複数の新規ゲームサーバーセッションを起動するときに、この機能があれば、 CVMインスタンス上で稼働する他のゲームサーバーセッションから受けるパフォーマンスへの影響を低減することができます。
  - ゲームサーバーセッションアクティベートのタイムアウト：新規ゲームサーバーセッションのアクティベートを許可する時間を制限します。設定可能なタイムアウトの時間制限は600sまたはそれ以下です。
![](https://main.qcloudimg.com/raw/c3bd554f125f7a73d5dea4ebb54d589a.jpg)

>- 許容並列プロセス数：1つの起動パスのバイナリーで起動する必要があるゲームプロセスの総数。
>- 最大並列起動ゲームサーバーセッション数：ゲームサーバーセッション状態の「アクティブ」な瞬間同時実行数。

### デプロイ設定
  - サーバータイプ：サーバーフリートを作成するサーバーマシンタイプ。
  - VPCネットワークのアクティブ化の有無：Tencent Cloud VPCネットワークをアクティブにし、あなたのVPC下のサーバー等にアクセスできるようにします。
![](https://main.qcloudimg.com/raw/5284d28b11f74f42a3a3c39e2fc2f45a.png)



 <span id="test12"></span>
### ネットワーク
  - ネットワーク：サーバープロセスのインバウンドトラフィックのアクセス権限を定義します。アクセスを許可する前に、フリートのために少なくとも1つまたは複数のポートを設定する必要があります。
    - ポート範囲：ゲームサーバーがインバウンド接続を許可するためのポート番号範囲を指定します。値は1025～60000の間とします。
    - プロトコル：フリートで使用したい通信プロトコルのタイプを選択します。TCPまたはUDPを選択できます。
    - IPアドレスの範囲：当該フリートの中のCVMインスタンスの有効IP アドレス範囲を指定します。CIDR表記を使用します（例：`0.0.0.0/0`、この例ではすべての人のアクセスへの接続試行を許可します）。
  - インスタンス数量： CVMサーバーのインスタンス数を指し、サーバーフリートの作成完了後に、サーバーフリートの詳細情報のスケーリングポリシーの画面で修正できます。
  - 保護ポリシー：時間限定保護、完全保護、保護しないが含まれます。
    開発者がプロセス終了のインターフェースを呼び出した時は自動的にプロセスを終了します。開発者がプロセス終了のインターフェースを呼び出さない時は、次の保護ポリシーが実行されます。
    - 時間限定保護：システムがスケールインをトリガーするか、またはプロセスに不備があるとき、システムは最長1時間でプロセスを終了します。値は5～1440の間、デフォルトは60分間です。
    - 完全保護： CVMインスタンスに現在実行中のプロセスがない時にのみ、終了できます。
    - 保護しない：システムがスケールインをトリガーするか、またはプロセスに不備があるとき、システムは最長5分以内にプロセスを終了します。
![](https://main.qcloudimg.com/raw/3478d408969d34e9daf49d199004c8df.png)

4. 上記の関連情報の設定の完了後、【作成】をクリックすると、サーバーフリートが作成されます。
5. 作成に成功すると、サーバーフリートのインターフェースで確認、削除などの操作が行えるようになります。同時に、サーバーフリートIDをクリックすれば、基本情報、イベント、インスタンスリスト、スケーリング、ゲームセッション、プロセス管理、ポートとプロトコル、アセット、VPCなどの情報を確認できます。




