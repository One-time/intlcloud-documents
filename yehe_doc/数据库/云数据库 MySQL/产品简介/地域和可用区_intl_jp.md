TencentDBをホスティングするデータセンターは世界の多くの場所に分布し、これらの位置のノードをリージョン（Region）と呼びます。各リージョンもまた複数のアベイラビリティーゾーン（Zone）で構成されています。
各リージョン（Region）はいずれも独立した地理的エリアです。各リージョン内にはアベイラビリティーゾーン（Zone）と呼ばれる複数の相互に隔離された場所があります。各アベイラビリティーゾーンは独立していますが、同一リージョンのアベイラビリティーゾーンは低遅延のプライベートネットワークリンクによって相互に接続されています。Tencent Cloudはユーザーがクラウドリソースをさまざまな場所に割り当てることをサポートしています。システム設定時には、リソースをさまざまなアベイラビリティーゾーンに配置し、単一障害点によって引き起こされるサービスの利用不可状態を防止するよう検討することをお勧めします、

リージョン、アベイラビリティーゾーンの名称は、データセンターがカバーする範囲を最も直接的に体現しています。お客様が分かりやすいように命名規則を以下のようにしています。
- リージョンの命名には【カバーする範囲＋データセンターが所在する都市】の組み合わせを採用し、前半部分で当該データセンターがカバーする能力を表し、後半部分で当該データセンターが所在するまたは隣接する都市を表しています。
- アベイラビリティーゾーンの命名には【都市 + 番号】の組み合わせを採用しています。

## リージョン
Tencent Cloudは、各リージョンを完全に隔離し、リージョン間で最大限の安定性とフォールトトレランスを確保しています。お客様のユーザーに最も近いリージョンを選択することをお勧めします。アクセスの遅延を減らし、ダウンロードスピードを向上させることができます。ユーザーがインスタンスを起動したり、インスタンスを表示したりするなどの操作は、リージョン属性によって識別されます。
クラウドサービスのプライベートネットワーク通信における注意事項：

- 同一リージョン下（同じアカウントかつ同じ VPC 内であること）のクラウドリソース間はプライベートネットワークで相互通信でき、 [プライベートIPアドレス](https://intl.cloud.tencent.com/document/product/213/5225)を使用して直接アクセスできます。
- 異なるリージョン間のネットワークは完全に隔離され、異なるリージョン間のクラウドサービスは、デフォルトではプライベートネットワークを介して相互通信できません。
- 異なるリージョン間のクラウド製品は、[パブリックIP]（https://intl.cloud.tencent.com/document/product/213/5224）を介してInternetにアクセスする方式で相互に通信できます。- 異なるVPC上のクラウド製品は、[CCN]（https://intl.cloud.tencent.com/document/product/1003）を介して相互に通信できます。この通信方式はより高速で安定しています。
- [CLB](https://intl.cloud.tencent.com/document/product/214) は、現在、デフォルトで同一リージョンのトラフィック転送をサポートし、ローカルリージョンのCVMをバインドします。[クロスリージョンバインディング]（https://intl.cloud.tencent.com/document/product/214/12014）機能が有効になっている場合、CVMをクロスリージョンでバインドするためのCLBをサポートできます。

## アベイラビリティーゾーン
アベイラビリティーゾーン（Zone）とは、Tencent Cloudが同一リージョン内で電源とネットワークが互いに独立している物理的なデータセンターです。ユーザーのビジネスのオンラインサービスの持続性を確保するため、アベイラビリティーゾーン間の障害を互いに隔離し（大規模な災害または大規模な電力設備の障害を除く）、障害の影響が拡散しないようにすることを目的としています。独立したアベイラビリティーゾーンでインスタンスを起動することにより、単一障害点の影響からアプリケーションを保護することができます。
ユーザーがインスタンスを起動する時は、指定リージョン下の任意のアベイラビリティーゾーンを選択可能です。ユーザーが高い信頼性を持つアプリケーションシステムを設計する必要がある場合（特定のインスタンスに障害が発生した時にもサービスの利用が持続可能）、クロスAZ型デプロイプラン（例：[CLB](https://intl.cloud.tencent.com/document/product/214)、[Elastic IP](https://intl.cloud.tencent.com/document/product/213/5733) など）を活用し、別のアベイラビリティーゾーン中のインスタンスに関連するリクエストの処理を代行させることが可能です。

## リージョンおよびアベイラビリティーゾーンのリスト
リージョン（Region）およびアベイラビリティーゾーン（Zone）の構成：
>?現在、パブリックネットワークアクセスは、次のリージョンをサポートしています。
>広州、上海、南京、北京、成都、重慶、中国香港、シンガポール、ソウル、東京、シリコンバレー、フランクフルト。

### 中国
<table class="table-striped">
<tbody>
<tr><th>地域</th><th>アベイラビリティーゾーン</th></tr>
<tr>
<td rowspan="6">華南地区（広州）<br> ap-guangzhou</td>
<td>広州1区（売り切れ）<br> ap-guangzhou-1</td></tr>	
<tr>
<td>広州2区<br> ap-guangzhou-2</td></tr>
<tr>
<td>広州3区<br> ap-guangzhou-3</td></tr>
<tr>
<td>広州4区<br> ap-guangzhou-4</td></tr>
<tr>
<td>広州6区<br> ap-guangzhou-6</td></tr>
<tr>
<td>広州7区<br> ap-guangzhou-7</td></tr>
<tr>
<td rowspan="5">華東地区（上海）<br>ap-shanghai</td>
<td>上海1区<br>ap-shanghai-1</td></tr>
<tr>
<td>上海2区<br>ap-shanghai-2</td></tr>
<tr>
<td>上海3区<br>ap-shanghai-3</td></tr>
<tr>
<td>上海4区<br>ap-shanghai-4</td></tr>
<tr>
<td>上海5区<br>ap-shanghai-5</td></tr>
<td rowspan="3">華東地区（南京）<br>ap-nanjing</td>
<td>南京1区<br>ap-nanjing-1</td></tr>
<tr>
<td>南京2区<br>ap-nanjing-2</td></tr>
<tr>
<td>南京1区<br>ap-nanjing-3</td></tr>
<tr>
<td rowspan="7">華北地区（北京）<br>ap-beijing</td>
<td>北京1区<br>ap-beijing-1</td></tr>
<tr>
<td>北京2区<br>ap-beijing-2</td></tr>
<tr>
<td>北京3区<br>ap-beijing-3</td></tr>
<tr>
<td>北京4区<br>ap-beijing-4</td></tr>
<tr>
<td>北京5区<br>ap-beijing-5</td></tr>
<tr>
<td>北京5区<br>ap-beijing-6</td></tr>
<tr>
<td>北京5区<br>ap-beijing-7</td></tr>
<tr>
<td rowspan="2">西南地区（成都）<br>ap-chengdu</td>
<td>成都1区<br>ap-chengdu-1</td></tr>
<tr>
<td>成都2区<br>ap-chengdu-2</td></tr>    
<tr>
<td >西南地区（重慶）<br>ap-chongqing</td>
<td>重慶1区<br>ap-chongqing-1</td></tr>
<tr>
<td rowspan="3">香港・マカオ・台湾地区（中国香港）<br>ap-hongkong</td>
<td>中国香港1区（中国香港のノードは中国香港・中国マカオ・中国台湾地域をカバーできる）<br>ap-hongkong-1</td></tr>
<tr>
<td>中国香港2区（中国香港のノードは中国香港・中国マカオ・中国台湾地域をカバーできる）<br>ap-hongkong-2</td></tr>
<tr>
<td>中国香港3区（中国香港のノードは中国香港・中国マカオ・中国台湾地域をカバーできる）<br>ap-hongkong-3</td></tr>
</tbody></table>	


### [その他の国および地域](id:InternationalArea)
<table class="table-striped">
<tbody>
<tr><th>地域</th><th>アベイラビリティーゾーン</th></tr>
<tr>
<td rowspan="3">東南アジア（シンガポール）<br>ap-singapore</td>
<td>シンガポール1区（シンガポールのノードは東南アジア地域をカバーできる）<br>ap-singapore-1</td></tr>
<tr>
<td>シンガポール2区（シンガポールのノードは東南アジア地域をカバーできる）<br>ap-singapore-2</td></tr>
<tr>
<td>シンガポール3区（シンガポールのノードは東南アジア地域をカバーできる）<br>ap-singapore-3</td>
</tr>
<td>東南アジア（ジャカルタ）<br>ap-jakarta</td>
<td>ジャカルタ1区（ジャカルタのノードは東南アジア地域をカバーできる）<br>ap-jakarta-1</td></tr>
<tr>
<td rowspan="2">東南アジア（バンコク）<br>ap-bangkok </td>
<td >バンコク1区 （バンコクのノードは東南アジア地域をカバーできる）<br>ap-bangkok-1</td>
<tr>
<td >バンコク2区 （バンコクのノードは東南アジア地域をカバーできる）<br>ap-bangkok-2</td>
<tr>
<td  rowspan="2">南アジア太平洋（ムンバイ）<br>ap-mumbai</td>
<td>ムンバイ1区（ムンバイのノードは南アジア太平洋地域をカバーできる）<br>ap-mumbai-1</td></tr>
<tr>
<td>ムンバイ2区（ムンバイのノードは南アジア太平洋地域をカバーできる）<br>ap-mumbai-2</td></tr>		
<tr>
<td rowspan="2">北東アジア（ソウル）<br>ap-seoul</td>
<td>ソウル1区（ソウルのノードは北東アジア地域をカバーできる）<br>ap-seoul-1</td></tr>
<tr>
<td>ソウル1区（ソウルのノードは北東アジア地域をカバーできる）<br>ap-seoul-2</td></tr>
<tr>
<td rowspan="2">北東アジア（東京）<br>ap-tokyo</td>
<td>東京1区（東京のノードは北東アジア地域をカバーできる）<br>ap-tokyo-1</td><tr>
<tr>
<td>東京2区（東京のノードは北東アジア地域をカバーできる）<br>ap-tokyo-2</td><tr>
<tr>
<td rowspan="2">米国西部（シリコンバレー）<br>na-siliconvalley</td>
<td>リコンバレー1区（シリコンバレーのノードは米国西部をカバーできる）<br>na-siliconvalley-1</td></tr>
<tr>
<td>リコンバレー1区（シリコンバレーのノードは米国西部をカバーできる）<br>na-siliconvalley-2</td></tr>
<tr>
<td rowspan="2">米国東部（バージニア）<br>na-ashburn</td>
<td>バージニア1区 （バージニアのノードは米国東部をカバーできる）<br>na-ashburn-1</td></tr>
<tr>
<td>バージニア2区 （バージニアのノードは米国東部をカバーできる）<br>na-ashburn-2</td></tr>
<tr>
<td>北米地区（トロント）<br>na-toronto</td>
<td>トロント1区（トロントのノードは北米地域をカバーできる）<br>na-toronto-1</td></tr>
<tr>
<td rowspan="2">欧州地区（フランクフルト）<br>eu-frankfurt</td>
<td>フランクフルト1区（フランクフルトのノードは欧州地域をカバーできる）<br>eu-frankfurt-1</td><tr>
<tr>
<td>フランクフルト2区（フランクフルトのノードは欧州地域をカバーできる）<br>eu-frankfurt-2</td></tr>
<tr>
<td >欧州地区（モスクワ）<br>eu-moscow</td>
<td>モスクワ1区（モスクワのノードはヨーロッパ地域をカバーできる）<br>eu-moscow-1</td></tr>
</tbody></table>

## リージョンとアベイラビリティーゾーンを選択する方法
クラウド製品を購入する際にはお客様に最も近い地域を選択することをお勧めします。アクセスの遅延を減らし、ダウンロードスピードを向上させることができます。
