 [VODコンソール](https://console.cloud.tencent.com/vod) で【データセンター】>【データ分析】を選択します。ここでは**アクセス状況**および**再生状況**の統計データを提供し、デフォルトでは「アクセス状況」画面が表示されます。

## アクセス状況

- アクセス状況の次元は、それぞれ今日、昨日、直近の7日、直近30日およびカスタマイズ可能な30日以内の任意の期間の統計次元になります。時間のほかに、ドメイン名、地区、キャリアなどの次元についても状況データをフィルタリングすることができます。
- データ概要指標は、指定された期間でのリクエスト総数（回数）および一意のIPアクセス総数（回数）です。
	- 一意のIPからのアクセス総数：指定期間サイクルにて、ログ内でソース元クライアントにアクセスするIPは重複排除して計算されます：時間区間が1日以下の場合、5分の粒度で重複排除されたIP数曲線が提供されます。ドメイン名の状況は1日のアクティブな量を重複排除してカウントされ、複数のドメイン名がある場合 、各ドメイン名の1日のアクティブな量が5分の粒度で累積されます。
	- リクエスト総数：ドメイン名が指定時間区間にあるときの総リクエスト数。
- リクエスト数（回数）、一意のIPアクセス数のトレンド（回数）、キャリアによるリクエスト数（回数）、リクエストの上位10地区データ（回数）をグラフィック表示。
- アクセス状況データには10分間程度の遅延があります。



## 再生状況

再生状況画面には**ファイル再生状況確認**、**再生回数上位100本のビデオ**、**再生トラフィック上位100本のビデオ**情報が表示されます。

- ファイル再生クエリー：VODのビデオFileIdに入力してクエリーをクリックすれば、そのビデオの再生回数および再生トラフィック量を得ることができます。VODは今日、昨日、直近7日間、直近30日間および30日以内の任意の期間のデータクエリーを提供します。ファイル再生状況データには3時間ほどの遅延があります。
- 再生回数上位100本のビデオ：指定期間にVODが提供する再生回数についての上位100の統計です。昨日および30日以内の任意の期間のデータを確認できます。再生回数上位100本のビデオデータは当日11時に前日の統計データを確認できます。
- 再生トラフィック上位100本のビデオ：指定期間にVODが提供する再生トラフィックにおける上位100の統計です。昨日および30日以内の任意の期間のデータを確認できます。再生トラフィック上位100本のビデオデータは当日11時に前日の統計データを確認できます。
