全リンク、即ち音声ビデオデータが送信側で生成されて受信側で処理されるまでの全てのリンク段階の状況は、音声ビデオ通話がスムーズに行われることを保証する必要があり、その大きな原則は、「良好なネットワーク」+「安定したデバイス」です。このため、開発者はユーザーの通話の全リンクを検査する時に、まずこの2つから開始します。

## 操作手順

1. TRTCコンソールにログインし、【[監視ダッシュボード](https://console.cloud.tencent.com/trtc/monitor)】で確認したいルームを選択します。
2. ルームID または右側の【通話詳細の確認】をクリックして、[通話詳細](https://intl.cloud.tencent.com/document/product/647/39070)画面に入ります。
3. 受信/送信側データの表示欄から、確認したいユーザーIDを選択して、次の方法で全リンク詳細画面に入り、2つのユーザー間の全リンク詳細を確認します。
	- 【受信側ビュー】では、右側の【送信側を選択して詳細を確認】をクリックして指定した送信側ユーザーIDを選択します。
	- 【送信側ビュー】では、右側の【詳細を確認】をクリックします。




## データの解説

全リンク詳細画面に表示されるデータは、【ビデオ】、【音声】、【画面共有】の3種類に分かれており、送信側と受信側のそれぞれ個別のリンクのデータを確認することができます。
全リンクの詳細については、[ネットワーク状況の分析](#internet)と[デバイス状態の確認](#equipment) の2つの側面から分析できます。

[](id:internet)
### ネットワーク状況の分析
理想的な状況のネットワーク転送は、パケットロスや遅延がなく、高帯域幅ですが、実際の状況では、往々にして多かれ少かれパケットロス、転送遅延、不安定な状況が存在し、ネットワーク帯域幅にも制限があります。よってネットワーク状況を分析する時は次の部分を重点的に注目する必要があります。

[](id:packet_loss)
#### ネットワークパケットロス
ネットワークにパケットロスが出現すると、データチャートに赤線で表示されます。

| パケット損失率                         | ネットワーク状態の説明             |
| ------------------------------ | ------------------------ |
| = 0                            | 最良                     |
| < 2%                           | 基本的に良好                 |
| &gt; 5%                        | 不良                     |
| &gt; 10%（または持続的なパケットロスが発生） | 現在のネットワークに比較的深刻な輻輳が存在します |

[](id:bit_rate)
#### ビットレート
正常な状況下では、ビデオとオーディオのビットレートは変動範囲±10%以内の曲線です。**ビットレートの急激な低下、または30%を超える変動が出現した場合は、現在のネットワークに輻輳またはジッターが発生していることを表します**。
> ! 画面共有の画面のGOPは長いため（5秒～10秒）、正常な状況では安定した周期のピークとボトムのある曲線となり、キーフレームがある時は、対応するピークがあります。

- 画面共有上りビットレートとネットワークパケットロス。
- 画面共有のビットレート曲線には安定した周期のピークがあります。

[](id:frame_rate)
#### フレームレート
正常な状況では、ビデオフレームレートは通常15フレーム以上（画面共有のフレームレートは一般的に5フレーム～10フレーム）で、かつ安定して維持されます。**フレームレートが5フレームを超える変動が出現、またはフレームレートが抜け落ちて10フレーム以下になって回復しない状態が続く時は、通常、現在のネットワークに輻輳またはジッターが発生し**、ユーザーは主観的にラグを感じます。過度に低いフレームレートが出現すると、データチャートに赤線で表示されます。

- ビデオ上りフレームレート：取得と送信のフレームレートに分かれます。
- ビデオレンダリングフレームレート：フレームレートが低い状況は赤線で表示され、ラグの期間が表記されます。


[](id:equipment)
### デバイス状態の確認

デバイスの安定して正常な作動は、音声ビデオ通話を保証する基盤です。デバイス状態が良好な通話は、システムリソースの使用率が低く、デバイス使用が優先されず、データ取得も干渉しません。デバイス状態を確認する時は、優先的に次の情報を確認します。

[](id:cpu)
## CPU占有率
CPU使用率は、システム全体のCPU使用率およびアプリのCPU使用率を表示し、正常な状況下ではシステム全体のCPU使用率は <50%で、低いほど良くなります。**システム全体のCPU使用率が>85%の時は、プログラムが応答しないまたはレスポンス遅延などの状況が発生しやすくなります。この時には赤線で表示されます**。

[](id:voice)
#### 音量レベル
- 音声**集音音量**は送信側がマイクから取得したデータの音量となり、**集音音量の大きさに数値の変動があればマイクが正常に音声を集音し、即ちデバイスが正常に作動していることの説明となります**。
- 音声**再生音量**は受信側が、レンダリングされたデータをデコードした後にスピーカーに送信する音量の大きさで、**再生音量に数値の変動があるとSDKが音声をスピーカーに送信したこと、即ちデバイスの作動が正常であることの説明となります**。

正常な音量の大きさは一般的に40dB～80dBの間で、40dBを下回る時は音声の音量が小さいことの説明となります。ユーザーが音声を聞き取れない場合、携帯電話のミュートをオンにしてないか、またはハードウェアが故障していないかを検査する必要があります。

[](id:resolution)
#### 解像度
ビデオと画面共有の解像度は補助的な情報で、主にRelayed live streamingおよびレコーディングファイルを再生するための判断に用いられます。ビデオの解像度に変動がある場合、[CDN](https://intl.cloud.tencent.com/product/cdn) 経由でRelayed live streamingを視聴する視聴者またはビデオ再生を視聴する視聴者（特にWebユーザー）には、画面のフリーズ、ぼやけるなどの再生装置との互換性による問題が存在する可能性があります。



>? [解像度](#resolution)、[ビットレート](#bit_rate) 、[フレームレート](#frame_rate)には一定の配合関係が存在します。通常、解像度が固定されている時、ビットレートが高いほど、画面は鮮明になります。またビットレートが固定の場合は、解像度が大きいほど、画面がぼやけます。解像度、ビットレート、フレームレートのパラメータを適切に設定することによって、より良いビデオ画質を実現できます。

#### クライアントのイベントのチェック
クライアントのイベントに対応するのがSDKを呼び出すAPPのメソッドの操作です。通常はソフトウェアのトラブルの特定やbugの分析の補助に用いられ、ユーザーが使用した操作手順を分析することで、対応するシーンを再現します。クライアントのイベントについては、次の状況に重点的に注目します。

- 入室、退室イベント。
- カメラまたはマイクのオン、オフ。
- デバイスの変更：カメラの切り替え、イヤホンの着脱、Bluetooth対応イヤホンの接続など。
- プッシュまたは再生の開始、停止。
- ミュート/ミュート解除の操作、静止画/静止画の解除。
- ネットワーク切り替え：4GからWIFIへの切り替えなど。

【詳細なイベントの確認】をクリックして、詳細なイベントリストに入り、クライアント上での主要なイベント操作のプロセスを確認できます。
