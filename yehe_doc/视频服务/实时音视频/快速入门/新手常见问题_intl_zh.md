
<h3 id="UserSig">什么是 UserSig？</h3>

UserSig 是腾讯云设计的一种安全保护签名，目的是为了阻止恶意攻击者盗用您的云服务使用权。
目前，腾讯云的实时音视频（TRTC）、即时通信（IM）以及移动直播（MLVB）等服务都采用了该套安全保护机制。要使用这些服务，您都需要在相应 SDK 的初始化或登录函数中提供 SDKAppID，UserID 和 UserSig 三个关键信息。
其中 SDKAppID 用于标识您的应用，UserID 用于标识您的用户，而 UserSig 则是基于前两者计算出的安全签名，它由 **HMAC SHA256** 加密算法计算得出。只要攻击者不能伪造 UserSig，就无法盗用您的云服务流量。
UserSig 的计算原理如下图所示，其本质就是对 SDKAppID、UserID、ExpireTime 等关键信息进行了一次哈希加密：
```Cpp
//UserSig 计算公式，其中 secretkey 为计算 usersig 用的加密密钥

usersig = hmacsha256(secretkey, (userid + sdkappid + currtime + expire + 
                                 base64(userid + sdkappid + currtime + expire)))
```


[](id:que2)
### 实时音视频最多可以同时创建多少个房间？
支持同时并发存在4294967294个房间，累计房间数量无限制。


[](id:que3)
### 实时音视频延时大约多少？
全球端到端平均延时小于300ms。


[](id:que4)
### 实时音视频接入 PC 端是否支持屏幕分享功能？
支持，您可以参考如下文档：
- [屏幕分享（Windows）](https://intl.cloud.tencent.com/document/product/647/37335)
- [屏幕分享（Mac）](https://intl.cloud.tencent.com/document/product/647/37336)
- [屏幕分享（Web）](https://intl.cloud.tencent.com/document/product/647/35163)

屏幕分享接口详情请参见 [Windows（C++）API](https://intl.cloud.tencent.com/document/product/647/35131) 或 Windows（C#）API。另外，您也可以使用 [Electron 接口](https://intl.cloud.tencent.com/document/product/647/35141)。


[](id:que5)
### TRTC 支持哪些平台？
支持的平台包括 iOS、Android、Windows(C++)、Windows(C#)、Mac、Web、Electron，更多详情请参见 [平台支持](https://intl.cloud.tencent.com/document/product/647/35078)。

[](id:que6)

### 实时音视频最多可以支持多少个人同时通话？
- 通话模式下，单个房间最多支持300人同时在线，最多支持50人同时开启摄像头或麦克风。
- 直播模式下，单个房间支持10万人以观众身份在线观看，最多支持50人以主播身份开启摄像头或麦克风。


[](id:que7)
###  TRTC 怎么实现直播场景类应用？
TRTC 专门针对在线直播场景推出了10万人低延时互动直播解决方案，能保证主播与连麦主播的最低延时到200ms，普通观众的延时在1s以内，并且超强的抗弱网能力适应移动端复杂的网络环境。
具体操作指引请参考 [跑通直播模式](https://intl.cloud.tencent.com/document/product/647/35107)。



[](id:que8)
### TRTC 直播支持什么角色？有什么区别？
直播场景（TRTCAppSceneLIVE 和 TRTCAppSceneVoiceChatRoom）支持 TRTCRoleAnchor（主播）和 TRTCRoleAudience（观众）两种角色，区别是主播角色可以同时上行、下行音视频数据，观众角色只支持下行播放其他人的数据。您可以通过调用 switchRole() 进行角色切换。


[](id:que9)
### TRTC 房间支不支持踢人、禁止发言、静音？  
支持。
- 如果是简单的信令操作，可以使用 TRTC 的自定义信令接口 sendCustomCmdMsg，开发者自己定义相应的控制信令，收到控制信令的通话方执行对应操作即可。例如，踢人就是定义一个踢人的信令，收到此信令的用户就自行退出房间。
- 如果是需要实现更完善的操作逻辑，建议开发者通过 [即时通信 IM](https://intl.cloud.tencent.com/document/product/1047) 来实现相关逻辑，将 TRTC 的房间与 IM 群组进行映射，在 IM 群组中收发自定义消息来实现相应的操作。


[](id:que10)
### TRTC 音视频流是否支持通过 CDN 拉流观看？ 
支持，详情请参见 [实现 CDN 直播观看](https://intl.cloud.tencent.com/document/product/647/35242)。


[](id:que11)
### 在 iOS 端是否支持 Swift 集成？
支持，直接按照支持集成三方库的流程集成 SDK 即可，还可以参考 [跑通Demo(iOS&Mac)](https://intl.cloud.tencent.com/document/product/647/35086)。


[](id:que12)
### Web 端 SDK 的支持哪些浏览器？  
目前主要在桌面版 Chrome 浏览器、桌面版 Safari 浏览器以及移动版的 Safari 浏览器上有较为完整的支持，其他平台（例如 Android 平台的浏览器）支持情况均比较差，具体详情请参见 [支持的平台](https://intl.cloud.tencent.com/document/product/647/41664)。
您可以在浏览器打开 [WebRTC 能力测试](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html) 测试是否完整的支持 WebRTC 的功能。


[](id:que13)
### Web 端 SDK 日志中报错 NotFoundError、NotAllowedError、NotReadableError、OverConstrainedError 以及 AbortError 分别是什么意思？


| 错误名 | 描述 | 处理建议 |
|---------|---------|---------|
| NotFoundError  | 找不到满足请求参数的媒体类型（包括音频、视频、屏幕分享）。<br>例如：PC 没有摄像头，但是请求浏览器获取视频流，则会报此错误。   | 建议在通话开始前引导用户检查通话所需的摄像头或麦克风等设备，若没有摄像头且需要进行语音通话，可在 [TRTC.createStream({ audio: true, video: false })](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createStream) 指明仅采集麦克风。 |
| NotAllowedError | 用户拒绝了当前的浏览器实例的访问音频、视频、屏幕分享请求。 | 提示用户不授权摄像头/麦克风访问将无法进行音视频通话。|
| NotReadableError  | 用户已授权使用相应的设备，但由于操作系统上某个硬件、浏览器或者网页层面发生的错误导致设备无法被访问。  | 根据浏览器的报错信息处理，并提示用户“暂时无法访问摄像头/麦克风，请确保当前没有其他应用请求访问摄像头/麦克风，并重试”。|
| OverConstrainedError|   cameraId/microphoneId 参数的值无效。 | 请确保 cameraId/microphoneId 传值正确且有效。|
| AbortError  | 由于某些未知原因导致设备无法被使用。| - |


更多详情请参考 [initialize](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html?#initialize)。


[](id:que14)
### 怎么确认 Web 端 SDK 是否能正常获取到设备（摄像头/麦克风）列表？
1. 检查浏览器是否能够正常使用设备：
直接在页面打开控制台，输入 `navigator.mediaDevices.enumerateDevices()` 确认能否获取到设备列表。
 - 如果正常获取到设备会返回一个 Promise，里面会有 MediaDeviceInfo 对象数组，数组里的每个对象对应一个可用的媒体设备。
 - 如果枚举失败，Promise 将返回 rejected，说明浏览器都没有识别到设备，需检查浏览器或设备。
2. 如果能获取设备列表，则输入 `navigator.mediaDevices.getUserMedia({ audio: true, video: true })` 确认能否正常返回 MediaStream 对象，不能正常返回说明浏览器没有获取到数据，需检查浏览器的配置。




[](id:que17)
### 直播、互动直播、实时音视频以及旁路直播有什么区别和关系？
- **直播**（关键词：一对多，RTMP/HLS/HTTP-FLV，CDN）
 直播分为推流端、播放端以及直播云服务，云服务使用 CDN 进行直播流的分发。推流使用的是通用标准的协议 RTMP，经过 CDN 分发后，播放时一般可以选择 RTMP、HTTP-FLV 或 HLS（H5 支持）等方式进行观看。
- **互动直播**（关键词：连麦、PK）
 互动直播是一种业务形式，指主播与观众之间进行互动连麦，主播与主播之间进行互动PK的一种直播类型。
- **实时音视频**（关键词：多人互动，UDP 私有协议，低延时）
 实时音视频（Tencent Real-Time Communication，TRTC）主要应用场景是音视频互动和低延时直播，使用基于 UDP 的私有协议，其延迟可低至100ms，典型的场景就是 QQ 电话、腾讯会议、大班课等。 腾讯云实时音视频（TRTC）覆盖全平台，除了 iOS/Android/Windows 之外，还支持 WebRTC 互通，并且支持通过云端混流的方式将画面旁路直播到 CDN。
- **旁路直播**（关键词：云端混流，RTC 旁路转推，CDN）
 旁路直播是一种技术，指的是将低延时连麦房间里的多路推流画面复制出来，在云端将画面混合成一路，并将混流后的画面推流给直播 CDN 进行分发播放。 


[](id:que18)
### TRTC 如何查看通话时长和使用量？  
可在实时音视频控制台的【[用量统计](https://console.cloud.tencent.com/trtc/statistics)】页面查看。



[](id:que19)
### TRTC 出现卡顿怎么排查？
可以通过对应的 RoomID、UserID 在实时音视频控制台的【[监控仪表盘](https://console.cloud.tencent.com/trtc/monitor)】页面查看通话质量：
- 通过接受端视角查看发送端和接收端用户情况。
- 查看发送端和接收端是否丢包率比较高，如果丢包率过高一般是网络状况不稳定导致卡顿。
- 查看帧率和 CPU 占用率，帧率比较低和 CPU 使用率过高都会导致卡顿现象。


[](id:que20)
### TRTC 出现画质不佳，模糊、马赛克等现象怎么排查？
- 清晰度主要和码率有关，检查 SDK 码率是否配置的比较低，如果高分辨率低码率容易产生马赛克现象。
- TRTC 会通过云端 QOS 流控策略，根据网络状况动态调整码率、分辨率，网络比较差时容易降低码率导致清晰度下降。
- 检查进房时使用的 VideoCall 模式还是 Live 模式，针对通话场景 VideoCall 模式主打低延时和保流畅，所以在弱网情况下会更容易牺牲画质确保流畅，对画质更加看重的场景建议使用 Live 模式。

[](id:que21)
### 如何查询 SDK 最新版本号？
- 若您使用自动加载的方法，`latest.release` 为匹配最新版并进行自动加载，不需要对版本号进行修改。具体集成方法请参见 [一分钟集成 SDK](https://intl.cloud.tencent.com/document/product/647/35092)。
- 当前 SDK 最新版本号可通过发布日志查看，具体请参见：
  - iOS & Android 端，请参见 [发布日志（App）](https://intl.cloud.tencent.com/document/product/647/39426)。
  - Web 端，请参见 [发布日志（Web）](https://intl.cloud.tencent.com/document/product/647/39779)。
  - Electron 端，请参见 [发布日志（Electron）](https://intl.cloud.tencent.com/document/product/647/38702)。




