## 작업 시나리오
Tencent Cloud의 네트워크는 [기본 네트워크와 VPC](https://intl.cloud.tencent.com/document/product/215/31807)로 구분되며, 사용자에게 서로 다른 품질의 서비스를 제공하고 있습니다. 이를 바탕으로 보다 유연한 네트워크 관리를 위해 다음과 같은 서비스를 제공합니다.
- **네트워크 변경**
  - 기본 네트워크를 VPC로 전환: 단일 CDB 마스터 인스턴스의 기본 네트워크를 VPC로 전환할 수 있습니다.
  - VPC A를 VPC B로 전환: 단일 CDB 마스터 인스턴스의 VPC A를 VPC B로 전환할 수 있습니다.
- **사용자 정의 IP 포트 설정**
 - 마스터 인스턴스 IP 사용자 정의: 인스턴스 상세 페이지에서 마스터 인스턴스 IP와 포트에 대한 사용자 정의를 지원합니다.
 - 읽기 전용 인스턴스 IP 사용자 정의: 인스턴스 상세 페이지에서 읽기 전용 인스턴스 IP와 포트에 대한 사용자 정의를 지원합니다.

##  주의 사항
- 네트워크를 전환하면 해당 인스턴스의 내부 IP가 변경될 수 있습니다. 기존 IP 주소의 회수 시간이 지나면 기존 액세스 IP는 유효하지 않으므로, 클라이언트 프로그램을 즉시 변경하시기 바랍니다.
기존 IP 주소의 보관 시간은 기본 24시간이며, 최대 168시간까지 지원됩니다. 기존 IP 주소의 회수 시간을 0시간으로 설정하면 네트워크 전환 후 기존 IP 주소가 즉시 회수됩니다.
- 기본 네트워크를 VPC로 전환한 후에는 다시 되돌릴 수 없으며, CDB를 VPC로 변경한 후에는 다른 VPC 및 기본 네트워크의 클라우드 서비스와 통신되지 않습니다.
- 전환한 CDB가 마스터 인스턴스이고 읽기 전용 인스턴스가 마운트되어 있다면, 마스터 인스턴스의 네트워크 전환 후, 마운트된 읽기 전용 인스턴스는 마스터 인스턴스에 따라 네트워크가 자동으로 전환되지 않으며 수동으로 변경해야 합니다.

## 작업 순서
### 네트워크 전환
1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb) 로그인 후, 인스턴스 리스트에서 인스턴스 ID 또는 '작업' 열의 [관리]를 클릭하여 인스턴스 상세 페이지로 이동합니다.
2. 인스턴스 기본 정보의 '소속 네트워크'에서 네트워크 간 전환 유형에 따라 [VPC 네트워크로 변경] 혹은 [네트워크 변경]을 클릭합니다.
3. 팝업된 대화 상자에서 VPC 및 해당하는 서브넷을 선택한 후 [확인]을 클릭합니다.
>?
>- IP 주소를 지정하지 않았다면 시스템에서 자동으로 할당합니다.
>- 타깃 VPC는 MySQL 인스턴스가 위치한 리전의 VPC 네트워크만 선택할 수 있습니다.
>- CVM이 있는 VPC를 선택하시길 권장합니다. 그러지 않으면, CVM에서는 내부 네트워크를 통해 MySQL(2개의 VPC 사이에 [피어링 연결](https://intl.cloud.tencent.com/document/product/553/18827)혹은 [CCN](https://intl.cloud.tencent.com/document/product/1003/30049)을 생성한 경우는 제외)에 액세스할 수 없습니다.
>
   - **기본 네트워크를 VPC로 변경**
![](https://main.qcloudimg.com/raw/ba78ed608b83c2f553cb72350b726491.png)
   - **VPC를 VPC로 변경**
![](https://main.qcloudimg.com/raw/d0df57066adb8398e599a6206db7cd56.png)
4. 인스턴스 상세 페이지로 돌아가면 인스턴스의 소속 네트워크를 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/5342a64814664fa784e256ecbd6f934f.png)

### IP 포트 사용자 정의
1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 후, 인스턴스 리스트에서 인스턴스 ID 또는 '작업' 열의 [관리]를 클릭하여 인스턴스 상세 페이지로 이동합니다.
2. 인스턴스 기본 정보의 '내부 네트워크 주소', '내부 네트워크 포트'에서 <img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;">를 클릭합니다.
>!내부 네트워크 주소와 포트를 변경하면 현재 액세스 중인 데이터베이스 작업에 영향을 줍니다.
3. 팝업된 대화 상자에서 IP 또는 포트를 사용자 정의하고, 오류가 없는지 확인한 다음 [확인]을 클릭합니다.
