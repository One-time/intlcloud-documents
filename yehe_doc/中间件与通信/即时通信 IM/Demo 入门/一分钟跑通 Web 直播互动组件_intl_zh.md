TWebLive 即腾讯云 Web 直播互动组件，是腾讯云终端研发团队推出的一个新的 SDK，集成了腾讯云实时音视频 TRTC、腾讯云即时通信以及腾讯云超级播放器 TCPlayer，覆盖了 Web 直播互动场景常见的功能（如推流、开/关麦、开/关摄像头、微信分享观看、聊天点赞等），并封装了简单易用的 [API](https://web.sdk.qcloud.com/component/tweblive/doc/zh-cn/TWebLive.html)，接入后可快速实现 Web 端推流、拉流以及实时聊天互动功能。您可以进入 [Demo](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html) 来体验。

## TWebLive 优势
开发者接入此 [TWebLive SDK](https://www.npmjs.com/package/tweblive)，可彻底替代 Flash 推流方案，极大地降低 Web 推流、Web 低延时观看、CDN 观看以及实时聊天互动（或弹幕）的实现复杂度和时间成本，下面我们通过举例来进行说明。

<dx-tabs>
::: 推流
当需要推流时，创建 Pusher（推流）对象，最简单的推流仅需3步：
<dx-codeblock>
::: html html

<div id="pusherView" style="width:100%; height:auto;"></div>
<script>
// 1、创建 Pusher（推流）对象
let pusher = TWebLive.createPusher({ userID: 'your userID' });
// 2、设置渲染界面，且从麦克风采集音频，从摄像头采集视频（默认720p）
pusher.setRenderView({
  elementID: 'pusherView',
  audio: true,
  video: true
}).then(() => {

// 3、填入 sdkappid roomid 等信息，推流
  // url 必须以 `room://` 开头
  let url = `room://sdkappid=${SDKAppID}&roomid=${roomID}&userid=${userID}&usersig=${userSig}&livedomainname=${liveDomainName}&streamid=${streamID}`;
  pusher.startPush(url).then(() => {
    console.log('pusher | startPush | ok');
  });
}).catch(error => {
  console.error('pusher | setRenderView | failed', error);
});
</script>
:::
</dx-codeblock>
:::
::: 拉流
当需要拉流播放时，创建 Player（播放器）对象，最简单的拉流仅需3步：

<dx-codeblock>
::: html html

<div id="playerView" style="width:100%; height:auto;"></div>
<script>
// 1、创建 Player（播放器）对象
let player = TWebLive.createPlayer();

// 2、设置渲染界面
player.setRenderView({ elementID: 'playerView' });

// 3-1、您可以填入 flv 或 hls 等格式的 CDN 播放地址，此类 URL 必须以 `https://` 开头
let url = 'https://'
  + 'flv=https://200002949.vod.myqcloud.com/200002949_b6ffc.f0.flv' + '&' // 请替换成实际可用的播放地址
  + 'hls=https://200002949.vod.myqcloud.com/200002949_b6ffc.f0.m3u8' // 请替换成实际可用的播放地址

// 3-2、您也可以填入以 `room://` 开头的 WebRTC 播放地址，此类地址可以实现超低的播放延时
let url = `room://sdkappid=${SDKAppID}&roomid=${roomID}&userid=${userID}&usersig=${userSig}`;
player.startPlay(url).then(() => {
  console.log('player | startPlay | ok');
}).catch((error) => {
  console.error('player | startPlay | failed', error);
});
</script>
:::
</dx-codeblock>
:::
::: 聊天室
当主播和观众需要聊天互动时，创建 IM（即时通信）对象，最简单的消息收发仅需3步：

<dx-codeblock>
::: javascript javascript
// 1、创建 IM（即时通信）对象并监听事件
let im = TWebLive.createIM({
  SDKAppID: 0 // 接入时需要将0替换为您的即时通信应用的 SDKAppID
});
// 监听 IM_READY IM_TEXT_MESSAGE_RECEIVED 等事件
let onIMReady = function(event) {
  im.sendTextMessage({ roomID: 'your roomID', text: 'hello from TWebLive' });
};
let onTextMessageReceived = function(event) {
  event.data.forEach(function(message) {
    console.log((message.from || message.nick) + ' : ', message.payload.text);
  });
};
// 接入侧监听此事件，然后可调用 SDK 发送消息等
im.on(TWebLive.EVENT.IM_READY, onIMReady);
// 收到文本消息，上屏
im.on(TWebLive.EVENT.IM_TEXT_MESSAGE_RECEIVED, onTextMessageReceived);

// 2、登录 IM 服务
im.login({userID: 'your userID', userSig: 'your userSig'}).then((imResponse) => {
  console.log(imResponse.data); // 登录成功
  if (imResponse.data.repeatLogin === true) {
    // 标识账号已登录，本次登录操作为重复登录
    console.log(imResponse.data.errorInfo);
  }
}).catch((imError) => {
  console.warn('im | login | failed', imError); // 登录失败的相关信息
});

// 3、加入直播间
im.enterRoom('your roomID').then((imResponse) => {
  switch (imResponse.data.status) {
    case TWebLive.TYPES.ENTER_ROOM_SUCCESS: // 加入直播间成功
      break;
    case TWebLive.TYPES.ALREADY_IN_ROOM: // 已经在直播间内
      break;
    default:
      break;
  }
}).catch((imError) => {
  console.warn('im | enterRoom | failed', imError); // 加入直播间失败的相关信息
});
:::
</dx-codeblock>
:::
</dx-tabs>

为了进一步降低开发者的开发和人力成本，我们在 TWebLive SDK 的基础上，提供了同时适配 PC 和移动端浏览器的 [Demo](https://github.com/tencentyun/TWebLive)，并开源到了 Github。开发者 fork&clone 项目到本地，稍作修改即可把 Demo 运行起来，也可集成到自己的项目部署上线。

## 操作步骤
### 步骤1：创建应用
<dx-tabs>
::: 基于实时音视频
在 [实时音视频 TRTC 控制台](https://console.cloud.tencent.com/trtc/app)，单击左侧导航栏【应用管理】>【创建应用】，输入您的应用名称，单击【确定】即可创建一个实时音视频应用。创建完毕后，请保存 SDKAPPID。
![](https://main.qcloudimg.com/raw/871c535f4b539ad7791f10d57ef0a9f3.png)

>?与此同时会自动创建一个 SDKAppID 相同的即时通信 IM 应用。
:::
::: 基于即时通信\sIM
1. 登录 [即时通信 IM 控制台](https://console.cloud.tencent.com/im)，单击【创建新应用】将弹出对话框。
![](https://main.qcloudimg.com/raw/15e61a874a0640d517eeb67e922a14bc.png)
2. 输入您的应用名称，单击【确认】即可完成创建。
![](https://main.qcloudimg.com/raw/7954cc2882d050f68cd5d1df2ee776a6.png)
3. 您可在 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) 总览页面查看新建应用的状态、业务版本、SDKAppID、创建时间以及到期时间。请记录 SDKAppID 信息。
:::
</dx-tabs>

### 步骤2：开通服务并获取密钥
<dx-tabs>
::: 基于实时音视频
1. 在 [实时音视频 TRTC 控制台](https://console.cloud.tencent.com/trtc/app)，单击左侧导航栏【应用管理】，在您创建的实时音视频应用上，单击【功能配置】进入应用详情。
![](https://main.qcloudimg.com/raw/bafd4eae90bd282b4f82421172d67e39.png)
2. 单击【启用旁路推流】，将旁路推流方式选择：全局自动旁路。旁路推流开启后，实时音视频 TRTC 房间里的每一路画面都配备一路对应的播放地址。
![](https://main.qcloudimg.com/raw/a153540779d95dff8a9b381b3566b36e.png)
>?如果不需要 CDN 直播观看，可略过开启旁路推流的步骤。
3. 单击【快速上手】，可查看密钥信息，请保存密钥。[](id:step2)
![](https://main.qcloudimg.com/raw/8ec16ab9cab85e324a347dea511f7e4e.png)
4. 在 [腾讯云直播控制台](https://console.cloud.tencent.com/live/) 配置播放域名并完成 CNAME 配置，详细操作指引请参见 [实现 CDN 直播观看](https://intl.cloud.tencent.com/document/product/647/35242) 文档。
>?如果不需要 CDN 直播观看，可略过配置播放域名步骤。
:::
::: 基于即时通信\sIM
1. 在 [即时通讯 IM 控制台](https://console.cloud.tencent.com/im) 总览页单击您创建完成的即时通信 IM 应用，随即跳转至该应用的基础配置页。在【基本信息】区域，单击【显示密钥】，复制并保存密钥信息。
![](https://main.qcloudimg.com/raw/610dee5720e94e324a48b44f4728816a.png)
  >!请妥善保管密钥信息，谨防泄露。
2. 在该应用的基础配置页，开通腾讯云实时音视频服务。
![](https://main.qcloudimg.com/raw/8fb2940618dfb8b7ea06eecd62212468.png)
:::
</dx-tabs>

### 步骤3：下载并配置 Demo
1. 请下载 [腾讯云 TWebLive 直播互动组件 Demo 工程](https://github.com/tencentyun/TWebLive)。
2. 打开 `TWebLive/dist/debug/GenerateTestUserSig.js` 文件，并设置相关参数：
 - SDKAPPID：请设置为 [步骤1](#step1) 中获取的实际应用 SDKAppID。
 - SECRETKEY：请设置为 [步骤2](#step2) 中获取的实际密钥信息。
 - PUSHDOMAIN：CDN观看，配置推流域名。（如果不需要 CDN 直播观看，可略过此配置）。
3. 在项目中通过 npm 安装最新版本的 tim-js-sdk、trtc-js-sdk、tweblive。如果项目已经集成有  tim-js-sdk 或 trtc-js-sdk，直接将其升级到最新版本即可。
<dx-codeblock>
::: 1 javascript
npm install tim-js-sdk --save
npm install trtc-js-sdk --save
npm install tweblive --save
:::
</dx-codeblock>
4. 在项目中引入 tweblive。
<dx-codeblock>
::: 1 javascript
import TWebLive from 'tweblive'
Vue.prototype.TWebLive = TWebLive
:::
</dx-codeblock>
5. 如果需要通过 script 标签外链的方式引入，需要将 tim-js.js、trtc.js、tweblive.js 拷贝至项目中，按顺序引入。
<dx-codeblock>
::: 1 javascript
<script src="./trtc.js"></script>
<script src="./tim-js.js"></script>
<script src="./tweblive.js"></script>
:::
</dx-codeblock>

>!
>- 本地计算 UserSig 的方式仅用于本地开发调试，请勿直接发布到线上，一旦您的 `SECRETKEY` 泄露，攻击者就可以盗用您的腾讯云流量。
>- 正确的 UserSig 签发方式是将 UserSig 的计算代码集成到您的服务端，并提供面向 App 的接口，在需要 UserSig 时由您的 App 向业务服务器发起请求获取动态 UserSig。更多详情请参见 [服务端生成 UserSig](https://intl.cloud.tencent.com/document/product/1047/34385)。

### 步骤4：运行 Demo
使用 Chrome 浏览器打开 `dist` 目录下的 `index.html` 文件即可运行 Demo。
>!
>
>- 一般情况下体验 Demo 需要部署至服务器，通过 `https://域名/xxx` 访问，或者直接在本地搭建服务器，通过 `localhost:端口`访问。
- 目前桌面端 Chrome 浏览器支持 TRTC 桌面浏览器 SDK 的相关特性比较完整，因此建议使用 Chrome 浏览器进行体验。
>- TWebLive 需要使用摄像头和麦克风采集音视频，在体验过程中您可能会收到来自 Chrome 浏览器的相关提示，单击【允许】即可。


## 架构与平台支持

### TWebLive 架构
TWebLive 架构设计如下图所示：
![](https://main.qcloudimg.com/raw/ab2b13a441da8b0631cc664f95ad18db.png)
Web 推流和 Web 低延时观看用到了 WebRTC 技术。

- 在移动端推荐使用小程序解决方案，微信和手机 QQ 小程序均已支持，由各平台的 Native 技术实现，音视频性能更好，且针对主流手机品牌进行了定向适配。
- 如果您的应用场景主要为教育场景，那么教师端推荐使用稳定性更好的 [Electron](https://intl.cloud.tencent.com/document/product/647/35097) 解决方案，支持大小双路画面，更灵活的屏幕分享方案以及更强大的弱网络恢复能力。
>?WebRTC 技术由 Google 最先提出，目前主要在桌面版 Chrome 浏览器、桌面版 Edge 浏览器、桌面版 Firefox 浏览器、桌面版 Safari 浏览器以及移动版的 Safari 浏览器上有较为完整的支持，其他平台（例如 Android 平台的浏览器）支持情况均较差。

### TWebLive 平台支持

|  操作系统   |          浏览器类型          | 浏览器最低版本要求 | 接收（播放） | 发送（上麦） |
| :---------: | :--------------------------: | :----------------: | :----------: | :----------: |
|   Mac OS    |     桌面版 Safari 浏览器     |        11+         |     支持     |     支持     |
|   Mac OS    |     桌面版 Chrome 浏览器     |        56+         |     支持     |     支持     |
|   Mac OS    |    桌面版 Firefox 浏览器     |        56+         |     支持     |     支持     |
|   Mac OS    |      桌面版 Edge 浏览器      |        80+         |     支持     |     支持     |
|   Windows   |     桌面版 Chrome 浏览器     |        56+         |     支持     |     支持     |
|   Windows   | 桌面版 QQ 浏览器（极速内核） |       10.4+        |     支持     |     支持     |
|   Windows   |    桌面版 Firefox 浏览器     |        56+         |     支持     |     支持     |
|   Windows   |      桌面版 Edge 浏览器      |        80+         |     支持     |     支持     |
| iOS 11.1.2+ |     移动版 Safari 浏览器     |        11+         |     支持     |     支持     |
| iOS 12.1.4+ |         微信内嵌网页         |         -          |     支持     |    不支持    |
|   Android   |       移动版 QQ 浏览器       |         -          |    不支持    |    不支持    |
|   Android   |       移动版 UC 浏览器       |         -          |    不支持    |    不支持    |
|   Android   |   微信内嵌网页（TBS 内核）   |         -          |     支持     |     支持     |
|   Android   |  微信内嵌网页（XWEB 内核）   |         -          |     支持     |    不支持    |

>! 由于 H.264 版权限制，华为系统的 Chrome 浏览器和以 Chrome WebView 为内核的浏览器均不支持 TRTC 桌面浏览器端 SDK 的正常运行。
[](id:sos)
## 注意事项

- 实时音视频应用与 IM 应用的 SDKAppID 一致，才能复用账号与鉴权。
- 本地计算 UserSig 的方式仅用于本地开发调试，请勿直接发布到线上，一旦 SECRETKEY 泄露，攻击者就可以盗用您的腾讯云流量。正确的 UserSig 签发方式是将 UserSig 的计算代码集成到您的服务端，并提供面向 App 的接口，在需要 UserSig 时由您的 App 向业务服务器发起请求获取动态 UserSig。更多详情请参见 [服务端生成 UserSig](https://intl.cloud.tencent.com/document/product/1047/34385)。

## 常见问题
<dx-accordion>
::: 1.\s查看密钥时只能获取公钥和私钥信息，要如何获取密钥？
2019年08月之前创建的 TRTC 以及 IM 应用（SDKAppID）默认使用区分公钥和私钥的 ECDSA-SHA256 签名算法，强烈建议您升级至 HMAC-SHA256 签名算法使用密钥。

- IM 升级方法请参见 [基本配置](https://intl.cloud.tencent.com/document/product/1047/34540)。
- TRTC 升级方法请参见 [UserSig 相关问题](https://intl.cloud.tencent.com/document/product/647/35166)。
:::
::: 2.\s出现客户端错误：“RtcError:\sno\svalid\sice\scandidate\sfound”该如何处理？
出现该错误说明 TRTC 桌面浏览器 SDK 在 STUN 打洞失败，请根据环境要求检查防火墙配置，配置完成后，您可以通过访问并体验官网 [Demo](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html) 检查配置是否生效。
- TCP 端口：8687
- UDP 端口：8000，8080，8800，843，443，16285
- 域名：qcloud.rtc.qq.com
:::
::: 3.\s出现客户端错误：“RtcError:\sICE/DTLS\sTransport\sconnection\sfailed”或\s“RtcError:\sDTLS\sTransport\sconnection\stimeout”该如何处理？
出现该错误说明 TRTC 桌面浏览器 SDK 在 STUN 打洞失败，请根据环境要求检查防火墙配置，配置完成后，您可以通过访问并体验官网 [Demo](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html) 检查配置是否生效。
- TCP 端口：8687
- UDP 端口：8000，8080，8800，843，443，16285
- 域名：qcloud.rtc.qq.com
:::
::: 4.\s出现10006\serror\s该如何处理？
如果出现 `"Join room failed result: 10006 error: service is suspended,if charge is overdue,renew it"`。请登录 [实时音视频控制台](https://console.cloud.tencent.com/rav)，单击您创建的应用，单击【帐号信息】，在帐号信息面板请确认您的实时音视频应用的服务状态是否为可用状态。
![](https://main.qcloudimg.com/raw/13c9b520ea333804cffb4e2c4273fced.png)
:::
::: 5.\sWebRTC\s低延时播放，iOS\s无法拉流播放？
1. 将 tweblive sdk 升级到 1.2.0。
2. 在调用 player.startPlay() 方法后，监听 PLAYER_AUTOPLAY_NOT_ALLOWED 浏览器不允许自动播放。
3. 监听到不能自动播放后，可显示一个播放按钮，在单击播放按钮时调用方法：[resumePlay()](https://web.sdk.qcloud.com/component/tweblive/doc/zh-cn/Player.html#resumePlay) 可恢复播放。
>?iOS 自动播放受限，参见 [自动播放受限处理建议](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-21-advanced-auto-play-policy.html)。
:::
</dx-accordion>

## 结语

本文为您介绍了腾讯云新的 Web 直播互动组件：TWebLive，通过接入此 SDK，开发者可以快速轻便地实现 Web 推流、Web 低延时观看、CDN 观看以及实时聊天互动（或弹幕）等功能，能够很好替换传统的 Flash 推流方案。

同时，提供详细的接入方案和 [在线 Demo](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html) 供您体验。目前 TWebLive 在主流的桌面浏览器上也有较好的支持，在移动端支持小程序的解决方案。

后续，我们会提供更全方位的直播功能服务，例如：推流端支持屏幕分享、图片消息互动、观众端多线路观看（WebRTC 低延时线路和 CDN 线路）、主播观众连麦互动等功能。

参考资料：

- [TWebLive 接口手册](https://web.sdk.qcloud.com/component/tweblive/doc/zh-cn/TWebLive.html)
- [Demo 体验](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html)
