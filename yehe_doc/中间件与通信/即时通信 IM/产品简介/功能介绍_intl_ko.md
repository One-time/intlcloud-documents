### 플랫폼 지원

다음 플랫폼은 모두 상호 운용성을 지원하며, 모든 멀티 단말 및 플랫폼에서 서비스를 제공합니다.

| 플랫폼    | SDK 및 호환성  | Demo     | 소스 코드     | UI 컴포넌트  |
| ------- | --------------| -------- | -------- | -------- |
| Android | JDK 1.6, Android SDK version 14 및 그 이후 버전 시스템 | 지원     | 지원     | 지원     |
| iOS     | iOS 8.0 및 그 이후 버전  | 지원     | 지원     | 지원     |
| Mac     | OS X 10.10 및 그 이후 버전  | 지원     | 지원     | -     |
| Windows | C, C++ 포함. Windows 7, Windows 8/8.1, Windows 10과 호환. 32비트 및 64비트 프로그램 연결 완벽 지원 | - | - | - |
| Web     | IE 11+, Chrome 7+, FireFox 3.6+, Opera 12+ 및 Safari 6+ 지원 | 지원     | - | - |
| 미니프로그램   | 지원   | 지원     | - | - |
|Unity|2020.2.7f1c1 및 그 이후 버전|지원|지원|-|
|Flutter|Flutter 2.0.12 버전|지원|지원|-|
|Electron|지원 |지원 |지원 |-|

### 글로벌 액세스

| 기능 유형       | 설명    |
| -------------- | -------------- |
| 글로벌 액세스 소개   | IM은 높은 연결성, 높은 신뢰성, 강력한 보안성을 갖춘 글로벌 네트워크 연결 채널 제공. 자체 개발 다중 최적 주소 지정 알고리즘 및 전체 네트워크 스케줄링 기능 보유. 해외 로그인 시 IM SDK는 가장 가까운 액세스 포인트 또는 가속 노드에 액세스함 |
| 중국 | 화남, 화북, 화동, 홍콩, 대만 등 |
| 중국 외 지역 | 아시아: 일본, 한국, 싱가포르, 인도, 태국, 말레이시아, 베트남, 필리핀, UAE, 인도네시아<br>유럽: 독일, 영국, 프랑스, 러시아, 이탈리아, 노르웨이, 스페인, 네덜란드<br>북미: 미국, 캐나다, 멕시코<br>남미: 브라질<br>오세아니아: 호주<br>아프리카: 남아공, 나이지리아 등 |


### 계정 기능

| 기능 유형       | 설명    |
| ------------ | -------------------------------------- |
| 계정 가져오기     | 계정 일괄 가져오기                           |
| 계정 비활성화     | UserSig 무효화                           |
| 계정 삭제     | 계정 일괄 삭제                       |
| 사용자 온라인 상태 | 온/오프라인 상태 관리(전제 조건: 사용자 로그인) |
| 계정 쿼리 | 계정 가져오기 여부 일괄 조회 |

### 멀티 단말 로그인

| 기능 유형       | 설명    |
| --------- | --------------------------------------------------------- |
| 단일 플랫폼 로그인     | Android, iPhone, iPad, Windows, Mac, Web 단일 플랫폼 로그인만 허용.              |
| 듀얼 플랫폼 로그인(기본 설정) | Android, iPhone, iPad, Windows, Mac 단일 플랫폼 로그인과 동시에 Web 로그인 허용            |
| 트리플 플랫폼 로그인     | Android, iPhone, iPad 단일 플랫폼 로그인, Windows 또는 Mac 단일 플랫폼 동시 로그인, Web 동시 로그인 허용 |
| 멀티 플랫폼 로그인     | Android, iPhone, iPad, Windows, Mac, Web 전체 플랫폼 동시 로그인 허용              |

>?[IM 콘솔](https://console.cloud.tencent.com/im)에 로그인하여 대상 애플리케이션이 위치한 행의 [애플리케이션 구성]을 클릭하고 [기능 설정] 페이지에서 멀티 단말 로그인을 설정합니다.

### 메시지 유형

| 기능 유형       | 설명    |
| ------------ | ----------------- |
| 텍스트 메시지     | 일반 텍스트로 구성된 메시지 내용     |
| 이미지 메시지     | 이미지 URL 주소, 사이즈, 이미지 크기 등 정보로 구성된 메시지 내용    |
| 이모티콘 메시지     | 개발자 사용자 정의 이모티콘 메시지   |
| 음성 메시지     | 음성 데이터는 지속시간 정보가 포함되어야 함(단위: 초)   |
| 지리적 위치 메시지 | 지리적 위치명, 경도, 위도 정보로 구성된 메시지 내용   |
| 텍스트 메시지     | 파일의 URL 주소, 크기, 형식 등 정보로 구성된 메시지 내용. 형식 제한 없으며 최대 100M 지원 |
| 쇼트 비디오 메시지   | 영상 파일의 URL 주소, 길이, 크기, 형식 등 정보로 구성된 메시지 내용. 최대 100M 지원 |
| 사용자 정의 메시지   | 홍바오 메시지, 가위바위보 등과 같은 개발자 사용자 정의 메시지 유형 |
| 시스템 알림 메시지 | 내부 시스템 알림 메시지 및 개발자 사용자 정의 시스템 알림 메시지 포함             |
|그룹 Tips 메시지|구성원 그룹 입/퇴장, 그룹 설명 정보 수정, 그룹 구성원 정보 변경 등 변화 알림 시스템 알림 메시지|
|메시지 병합|최대 300개의 메시지 병합 지원|



### 메시지 기능

| 기능 유형       | 설명    |
| -------- | -------- |
| 메시지 다운로드 | App 관리자는 이 인터페이스를 통해 지난 7일 일정 기간 동안의 App 내 모든 1:1 또는 그룹 메시지 기록을 가져올 수 있음 |
| 오프라인 메시지 | 사용자 로그인 후 백그라운드로 전환 시 IM이 다른 사용자가 보낸 메시지를 오프라인 푸시함. |
| 로밍 메시지 | 새 디바이스에서 로그인하면 서버가 (클라우드에) 저장한 메시지가 동기화되며, 기본적으로 7일 동안 보관되고 유료 연장 가능 |
| 멀티 단말 동기화 | 멀티 단말 메시지 동기화, 메시지 동시 수신 가능                               |
| 메시지 기록 | 로컬 메시지 기록 및 클라우드 메시지 기록 지원                               |
| 메시지 회수 | 성공적으로 전달된 메시지에 대해 기본적으로 2분 이내 메시지 회수 가능. 회수 작업은 1:1 및 그룹 채팅 메시지만 가능하며, 라이브 방송 채팅방(AVChatRoom)은 지원되지 않음 |
| 읽음 확인 | 1:1 채팅에서 상대방의 읽음 및 읽지 않음 상태 확인                           |
| 메시지 전달 | 다른 사용자 또는 그룹에 메시지 전달                                   |
| @기능    | 그룹 내의 @메시지와 일반 메시지는 본질적인 차이는 없으며, @대상자가 메시지를 받았을 때 UI에서 특별 처리함 |
| 입력 중 표시 | 온라인 메시징을 통해 구현 가능                                         |
| 오프라인 푸시 | Apple APNs, Xiaomi 푸시, Huawei 푸시, Meizu 푸시, OPPO 푸시, vivo 푸시, Google FCM 푸시 지원 |
| 메시지 삭제 | 메시지의 remove 메소드를 사용하여 로컬에서 메시지 삭제 가능                   |
| 홍바오 기능 | 홍바오 메시지는 @메시지와 유사, TIMCustomElem을 통해 구현 가능           |
|전체 푸시|REST API는 IM 통신 아키텍처를 기반으로 구현됨. 전체 푸시, 태그 푸시 및 속성 푸시 등 App 메시지 푸시 니즈 지원. 클라이언트단에서 SDK 온라인 푸시, 오프라인 푸시(Android 백그라운드 알림 및 APNs)으로 푸시 메시지 수신 가능|
|로컬 메시지 검색|친구 검색, 그룹 검색, 그룹 구성원 검색, 메시지 검색 및 대화별 그룹화 지원|


### 프로필 기능

| 기능 유형       | 설명    |
| ------------------ | ---------------- |
| 사용자 정보 설정   | 사용자가 자신의 닉네임, 인증 방법, 프로필 사진, 성별, 나이, 서명, 위치 등 정보를 설정 |
| 사용자 정보 가져오기  | 사용자 자신, 친구 및 낯선 사람에 대한 정보 보기    |
| 필드별 사용자 정보 가져오기 | 특정 필드에 따라 사용자 정보 가져오기       |
| 사용자 정의 사용자 정보     | 최대 20개의 사용자 정의 사용자 프로필 필드      |



### 관계망 기능

| 기능 유형       | 설명    |
| -------------------- | ---------------------- |
| 친구 찾기             | 사용자 계정 ID로 친구 찾기           |
| 친구 추가 요청         | 친구 추가 이유 작성 여부 선택 가능. 기본 설정 값: 작성하지 않음       |
| 친구 추가             | 친구 추가 요청 발송            |
|친구 가져오기|단방향 친구 일괄 가져오기 지원|
|친구 업데이트|사용자의 여러 친구 관계망 데이터 일괄 업데이트 지원|
| 친구 삭제             | 친구 추가 후 친구 삭제 가능         |
| 모든 친구 가져오기         | 모든 친구 가져오기. 기본 설정 값: 기본 정보만 가져오기       |
| 친구 동의/거부        | 친구 추가 요청 시스템 알림 수신 후 승인 또는 거부 가능   |
| 블랙리스트 추가     | 사용자 차단 기능. 기존 친구인 경우 친구 관계 해제    |
| 블랙리스트에서 제거           | 블랙리스트에서 사용자 제거              |
| 블랙리스트 가져오기       | 사용자 블랙리스트 가져오기                         |
| 친구 설명             | 친구 추가 완료 후 친구 설명 작성 가능                  |
| 친구 사용자 정의 프로필 설정   | 최대 20개의 친구 사용자 정의 필드              |
| 친구 그룹 만들기         | 그룹 생성 시 사용자를 동시 지정하여 그룹화 가능. 한 사용자를 여러 그룹에 추가 가능 |
| 친구 그룹 삭제         | 친구 그룹 삭제                       |
|친구 검증|친구 관계 일괄 검증 지원|
|블랙리스트 검증|블랙리스트 일괄 검증 지원|
| 그룹에 친구 추가     | 친구 그룹에 친구 추가                |
| 그룹에서 친구 제거     | 친구 그룹에서 친구 제거              |
| 친구 그룹 이름 바꾸기       | 친구 그룹 이름 바꾸기                      |
| 친구 그룹 정보 가져오기 | 친구 그룹 가져오기                   |
| 모든 친구 그룹 가져오기     | 모든 그룹 정보를 가져오기. 모든 친구 가져오기를 통해서도 그룹 정보를 가져올 수 있음 |
| 관계망 정보 저장       | SDK 관계망 데이터 저장 가능           |
| 친구 정보 변경 시스템 알림 | 친구 정보 변경에 대한 시스템 알림 수신 가능               |
| 관계망 변경 시스템 알림   | 관계망 변경에 대한 시스템 알림 수신 가능           |



### 그룹 기능
IM은 일반적인 사용 시나리오에 따라 다음 그룹 유형을 기본 설정합니다.
- 업무 그룹(Work): 사용자가 그룹 구성원인 친구의 초대를 받아 그룹에 입장할 수 있도록 합니다. 그룹 입장에는 초대받은 사람의 동의나 그룹 소유자의 승인이 필요 없습니다.
- 공개 그룹(Public): 그룹 소유자가 그룹 관리자를 지정할 수 있습니다. 그룹에 입장하기 위해서는 사용자가 그룹 ID를 검색하여 요청을 보내야 하며, 그룹 소유자 또는 관리자의 승인을 받아야 그룹에 입장할 수 있습니다.
- 회의 그룹(Meeting): 사용자가 자유롭게 입/퇴장할 수 있으며, 사용자 그룹 참여 전의 메시지 기록 보기를 지원합니다. 회의 그룹은 멀티미디어 회의, 온라인 교육 등 Tencent Real-Time Communication(TRTC) 제품 통합 시나리오에 적합합니다.
- 라이브 방송 그룹(AVChatRoom): 사용자가 자유롭게 입/퇴장할 수 있으며, 구성원 인원 제한 및 메시지 기록 저장 기능이 없습니다. Cloud Streaming Services(CSS)와 통합하여 댓글 자막 채팅 시나리오에 활용할 수 있습니다.

각 그룹 유형의 기본 기능 차이점은 다음과 같습니다.

<table>
   <tr>
      <th width="0px" style="text-align:center">기능 유형</td>
      <th width="0px" style="text-align:center">업무 그룹(Work)</td>
			 <th width="0px" style="text-align:center">공개 그룹(Public)</td>
       <th width="0px" style="text-align:center">회의 그룹(Meeting)</td>
			 <th width="0px" style="text-align:center">라이브 방송 그룹(AVChatRoom)</td>
   </tr>
   <tr>
      <td style="text-align:center">인원 제한</td>
      <td ><li>체험판: 20명/그룹</li><br><li>프로 버전: 기본 설정값: 200명/그룹, 최대 확장 가능 규모: 2000명/그룹</li><br><li>울티메이트 버전: 기본 설정값: 2000명/그룹, 최대 확장 가능 규모: 6000명/그룹</li></td>
			      <td><li>체험판: 20명/그룹</li><br><li>프로 버전: 기본 설정값: 200명/그룹, 최대 확장 가능 규모: 2000명/그룹</li><br><li>울티메이트 버전: 기본 설정값: 2000명/그룹, 최대 확장 가능 규모: 6000명/그룹</li></td>
						      <td ><li>체험판: 20명/그룹</li><br><li>프로 버전: 기본 설정값: 200명/그룹, 최대 확장 가능 규모: 2000명/그룹</li><br><li>울티메이트 버전: 기본 설정값: 2000명/그룹, 최대 확장 가능 규모: 6000명/그룹</li></td>
									      <td>무제한</td>
   </tr>
   <tr>
     <td>그룹 정보 수정</td>
     <td>그룹 구성원</td>
    <td><li>그룹 관리자</li><br><li>그룹 소유자</li><br><li>App 관리자</li></td>
    <td><li>그룹 소유자</li><br><li>App 관리자</li></td>
    <td>App 관리자</td>
   </tr>
	   <tr>
     <td>구성원 리스트</td>
     <td>전체보기</td>
    <td>전체보기</td>
    <td>전체보기</td>
    <td>300명 표시</td>
   </tr>
	   <tr>
     <td>그룹 해산</td>
     <td>App 관리자</td>
    <td><li>그룹 소유자</li><br><li>App 관리자</li></td>
    <td><li>그룹 소유자</li><br><li>App 관리자</li></td>
    <td><li>그룹 소유자</li><br><li>App 관리자</li></td>
   </tr>
	   <tr>
     <td>그룹 참여 신청</td>
     <td>미지원</td>
    <td>허용</td>
    <td>허용</td>
    <td>허용</td>
   </tr>
	   <tr>
     <td>그룹 참여 심사</td>
     <td>미지원</td>
    <td>심사 필요</td>
    <td>심사 안함</td>
    <td>심사 안함</td>
   </tr>
	   <tr>
     <td>그룹 초대</td>
     <td>초대 받은 자는 심사 필요 없음</td>
    <td>미지원</td>
    <td>미지원</td>
    <td>미지원</td>
   </tr>
	 	   <tr>
     <td>그룹 호스트 퇴장</td>
     <td>지원</td>
    <td>미지원</td>
    <td>미지원</td>
    <td>미지원</td>
   </tr>
	 	   <tr>
     <td>관리자 설정</td>
     <td>미지원</td>
    <td>지원</td>
    <td>지원</td>
    <td>미지원</td>
   </tr>
		 	   <tr>
     <td>구성원 제거</td>
    <td><li>그룹 소유자</li><br><li>App 관리자</li></td>
    <td><li>그룹 관리자</li><br><li>그룹 소유자</li><br><li>App 관리자</li></td>
    <td><li>그룹 관리자</li><br><li>그룹 소유자</li><br><li>App 관리자</li></td>
    <td>미지원</td>
   </tr>
		 	   <tr>
     <td>그룹 참여 전 메시지 기록 보기 지원 여부</td>
     <td>미지원</td>
    <td>미지원</td>
    <td>지원</td>
    <td>미지원</td>
   </tr>
		 	   <tr>
     <td>구성원 변경 알림</td>
     <td>전원</td>
    <td>전원</td>
    <td>없음</td>
    <td>전원</td>
   </tr>
		 	   <tr>
     <td>그룹 활성화</td>
     <td>메시지 활성화</td>
    <td>필요 없음</td>
    <td>필요 없음</td>
    <td>필요 없음</td>
   </tr>
	 	   <tr>
     <td>구성원 음소거</td>
     <td>미지원</td>
    <td>지원</td>
    <td>지원</td>
    <td>지원</td>
   </tr>
		 	   <tr>
     <td>읽지 않음 수</td>
     <td>지원</td>
    <td>지원</td>
    <td>지원</td>
    <td>미지원</td>
   </tr>
		 	   <tr>
     <td>게스트 신분으로 메시지 수신</td>
     <td>미지원</td>
    <td>미지원</td>
    <td>미지원</td>
    <td>지원</td>
   </tr>
		 	   <tr>
     <td>메시지 기록 보관</td>
     <td>지원</td>
    <td>지원</td>
    <td>지원</td>
    <td>미지원</td>
   </tr>
		 	   <tr>
     <td>기본 메시지 수신 옵션</td>
     <td>온/오프라인 푸시 메시지 수신</td>
    <td>온/오프라인 푸시 메시지 수신</td>
    <td>온라인 푸시 메시지만 수신</td>
    <td>온라인 푸시 메시지만 수신</td>
   </tr>
		 	   <tr>
     <td>그룹 가져오기</td>
     <td>지원</td>
    <td>지원</td>
    <td>지원</td>
    <td>미지원</td>
   </tr>
</table>




### IM 콘솔

Tencent Cloud [IM 콘솔](https://console.cloud.tencent.com/im)에서 필요에 따라 애플리케이션에 설정을 진행할 수 있습니다.

| 기능 유형       | 설명    |
| ------- | --------------------- |
| 애플리케이션 생성    | 애플리케이션 생성                  |
| 애플리케이션 업그레이드    | 패키지 버전 업그레이드               |
| SDK 다운로드  | 클라이언트단 SDK 다운로드            |
| 애플리케이션 설정    | 애플리케이션 설정 진행 가능               |
| 통계 및 분석    | 운영 데이터 조회                |
| 콜백 설정    | 서드 파티 콜백                 |
| 기능 설정    | 사용자 정의 필드 및 온라인 인스턴스 추가          |
| 그룹 관리    | 그룹 추가, 수정, 해산, 그룹 구성원 관리, 메시지 발송 |
| 개발자 보조 툴 | 웹에서 UserSig 생성        |
| 콘텐츠 필터링    | 불건전 메시지 식별 및 필터링          |



### 데이터 통계

IM 콘솔의 [통계 및 분석](https://console.cloud.tencent.com/im) 기능은 각종 차원의 데이터 통계 및 운영 데이터를 제공합니다.

| 통계 유형       | 설명    |
| -------- | ----------------- |
| 활성 사용자 수    | 서버와 연결한 중복 제거된 사용자 수  |
| 신규 등록 사용자 수  | 신규 등록 ID 수        |
| 총 등록 사용자 수  | 등록된 모든 사용자 수 보기         |
| 업스트림 메시지 수    | 시간대를 선택하여 업스트림 메시지 수 조회 가능     |
| 메시지 발송자 수   | 시간대를 선택하여 메시지를 보낸 사람 수 조회 가능    |
| 최대 동시 접속자 수 | 시간대를 선택하여 최대 동시 접속자 수 조회 가능  |
| 1대1 채팅 업스트림 메시지 수  | 시간대를 선택하여 1대1 채팅 업스트림 메시지 수 조회 가능   |
| 1대1 채팅 메시지 발송자 수  | 시간대를 선택하여 1대1 채팅 메시지 발송자 수 조회 가능   |
| 그룹 채팅 업스트림 메시지 수  | 시간대를 선택하여 그룹 채팅 업스트림 메시지 수 조회 가능  |
| 그룹 채팅 메시지 발송자 수  | 시간대를 선택하여 그룹 채팅 메시지 발송자 수 조회 가능 |
| 메시지 발송 그룹 수   | 시간대를 선택하여 메시지 발송 그룹 수 조회 가능    |
| 신규 그룹 수    | 시간대를 선택하여 신규 그룹 수 조회 가능     |
| 누적 그룹 수    | 시간대를 선택하여 누적 그룹 수 조회 가능     |
| 데이터 내보내기     | 시간대를 선택하여 데이터 내보내기 가능        |

### 실시간 모니터링
IM 콘솔의 [통계 및 분석](https://console.cloud.tencent.com/im) 기능은 각종 차원의 데이터 통계 및 운영 데이터를 제공합니다.

| 통계 유형       | 설명    |
| -------- | ---------- |
| 현재 온라인 사용자 수  | 실시간 온라인 인원     |
| 금일 1:1 메지시량  | 당일 1:1 총 메시지량   |
| 금일 일반 그룹 메시지량 | 당일 라이브 방송 그룹 외 총 메시지량 |
| 금일 라이브 방송 그룹 메시지량 | 당일 라이브 방송 그룹 총 메시지량  |

### 프라이빗 배포 지원
기업은 프라이빗 배포를 통해 회사 자체 서버에 시스템을 배포하고, 데이터를 로컬에 저장할 수 있습니다. IM은 기업의 프라이빗 버전의 배포, 구현 및 유지 관리를 지원하는 프라이빗 배포 기능을 제공합니다. 본 서비스가 필요하시면 [IM 프라이빗 서비스](https://intl.cloud.tencent.com/apply/p/itvi76h023)를 신청하시기 바랍니다.
>? 신청 시 Tencent Cloud 루트 계정 로그인이 필요합니다.
