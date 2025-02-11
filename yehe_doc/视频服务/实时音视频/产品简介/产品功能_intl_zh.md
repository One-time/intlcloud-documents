## 基础功能

<table>
<tr><th>功能</th><th width="50%">功能说明</th><th width="35%">常见应用场景</th><th>计费说明</th>
</tr>
<tr>
<td>视频通话</td>
<td><ul style="margin:0">
<li>即两人或多人视频通话，支持720P、1080P高清画质。
<li>单个房间最多支持300人同时在线，最多支持50人同时开启摄像头。</li>
</ul></td>
<td>1对1视频通话、300人视频会议、在线问诊、视频聊天、视频客服、视频面审、视频双录、在线理赔、视频狼人杀等。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/39788">视频通话计费说明</a></td>
</tr>
<tr>
<td>语音通话</td>
<td><ul style="margin:0">
<li>即两人或多人语音通话，支持 48kHz，支持双声道。</li>
<li>单个房间最多支持300人同时在线，最多支持50人同时开启麦克风。</li>
</ul></td>
<td>1对1语音通话、多人语音通话、语音聊天、语音会议、语音客服、狼人杀等。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/39787">语音通话计费说明</a></td>
</tr><tr>
<td>视频互动直播</td>
<td><ul style="margin:0">
<li>支持主播与观众视频连麦互动。</li>
<li>支持主播跨房间（跨直播间）PK。</li>
<li>支持平滑上下麦，切换过程无需等待，主播延时小于300ms。</li>
<li>单个房间可上麦人数无限制，最多支持50人同时连麦。</li>
<li>低延时直播模式下，支持10万观众同时播放，播放延时低至1000ms。</li>
<li>CDN 旁路直播模式下，观众数量无限制。</li>
</ul></td>
<td>视频低延时直播、十万人互动课堂、视频直播 PK、视频相亲房、互动课堂、远程培训、大型会议等。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/39786">视频互动直播计费说明</a></td>
</tr><tr>
<td>语音互动直播</td>
<td><ul style="margin:0">
<li>支持主播与观众语音连麦互动。</li>
<li>支持主播跨房间（跨直播间）PK。</li>
<li>支持平滑上下麦，切换过程无需等待，主播延时小于300ms。</li>
<li>单个房间可上麦人数无限制，最多支持50人同时连麦。</li>
<li>低延时直播模式下，支持10万观众同时播放，播放延时低至1000ms。</li>
<li>CDN 旁路直播模式下，观众数量无限制。</li>
</ul></td>
<td>语音低延时直播、语音直播连麦、语音直播 PK、语聊房、语音相亲房、K 歌房、FM 电台等。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/39785">语音互动直播计费说明</a></td>
</tr></table>


## 高级功能

| 功能           | 功能说明                                                     | 常见应用场景                     | 计费说明                                                     |
| -------------- | ------------------------------------------------------------ | -------------------------------- | ------------------------------------------------------------ |
| 互动连麦       | 支持连麦互动，观众可自由、平滑上下麦，切换过程无需等待。     | 互动直播、在线课堂、聊天房等。   | 使用互动连麦功能将产生基础服务用量，需支付 [基础服务费用](https://intl.cloud.tencent.com/document/product/647/34610)。 |
| 跨房 PK        | 也称作“跨直播间 PK”，多个主播跨房间互动 PK，观众观看。       | 秀场直播、PK 连麦、跨房授课等。  | 使用跨房 PK 功能将产生基础服务用量，需支付 [基础服务费用](https://intl.cloud.tencent.com/document/product/647/34610)。 |
| 屏幕分享       | 又称屏幕共享，支持将本地电脑桌面、窗口、画面区域分享给他人，例如 Microsoft PowerPoint 播放 PPT 的窗口。 | 在线课堂、PPT 共享、远程协助等。 | 使用屏幕分享功能将产生基础服务用量，需支付 [基础服务费用](https://intl.cloud.tencent.com/document/product/647/34610)。 |
| 服务端本地录制 | 服务端录制需要使用 Linux SDK。Linux SDK 暂未完全开放，如您需咨询或使用相关服务，请联系：colleenyu@tencent.com | 双录、存档、合规等。             | 使用服务端本地录制功能将产生基础服务用量，需支付 [基础服务费用](https://intl.cloud.tencent.com/document/product/647/34610)。 |
| 云端录制       | 采用旁路推流的方式使用 [云直播](https://intl.cloud.tencent.com/document/product/267) 的能力为您提供全程的云端录制功能（即录音/录像），并将录制下来的文件存储到 [云点播](https://intl.cloud.tencent.com/document/product/266) 平台，保证录制过程的可靠性和实时性。 | 双录、存档、合规等。             | 云端录制属于增值服务，需额外支付 [云端录制费用](https://intl.cloud.tencent.com/document/product/647/38385)。 |
| 云端混流转码    |使用 MCU 集群将 TRTC 房间内各路上行音视频流按需进行混流转码，转码后输出的音视频流可旁路推流至云直播进行云端录制或实现 CDN 直播观看。  | 多路画面按需混合、录制格式转换等。 |云端混流转码属于增值服务，需额外支付 [云端混流转码费用](https://intl.cloud.tencent.com/document/product/647/38929)。
| 高音质         | <li>支持48kHz采样的高音质。</li><li>支持真左右声道立体声音频，媲美纯正 CD 效果。</li> | 语音通话、视频通话、互动直播、语聊房、高音质 FM、音乐教学课、K 歌房、在线课堂等。 | 免费                                                         |
| 高画质         | 支持720P、1080P的高清画质视频。                              | 视频通话、互动直播、在线课堂等。                             | 免费                                                         |
| 3A 处理        | 由行业领先的 TRAE 音频引擎进行 3A 处理，在双讲、降噪等场景下提供更好的声音质量。3A 即 AEC（回声消除）、ANS（自动噪声抑制）、AGC（自动增益控制）。 | 所有语音场景。                                               | 免费                                                         |
| 基础美颜       | 支持基础的美颜功能，包括设置美白、磨皮、红润以及基本的滤镜效果。 | 视频通话、互动直播、在线课堂等。                             | 免费                                                         |
| BGM            | 支持将本地的 mp3、aac、wav 等格式的音乐文件作为人声的背景音乐。 | 语音通话、视频通话、互动直播、在线课堂、语聊房、K 歌房、FM 电台等。 | 免费                                                         |
| 音效           | 在通话过程中添加效果音，例如鼓掌、欢呼、吹口哨、嘘声等。     | 语音通话、视频通话、互动直播、语聊房、K 歌房、FM 电台等。    | 免费                                                         |
| 伴音伴奏       | 将本地播放的声音发送给他人，例如电脑上 QQ 音乐播放器播放的声音。 | 互动直播、在线课堂、语聊房、FM 电台等。                      | 免费                                                         |
| 变声           | 提供变声特效，例如萝莉、大叔、重金属等声音特效。             | 语音通话、视频通话、互动直播、语聊房、K 歌房、FM 电台等。    | 免费                                                         |
| 混响           | 提供混响效果，例如 KTV、小房间、音乐厅、浴室等混响效果。     | 语音通话、视频通话、互动直播、语聊房、K 歌房、FM 电台等。    | 免费                                                         |
| 音量大小回调   | 提供音量大小的数值，方便显示成波形动画或提示。               | 语音通话、视频通话、语聊房、FM 电台、K 歌房、人声检测等。    | 免费                                                         |
| 耳返           | 将本地录制的声音在本地的耳机中播放出来，让自己听到自己所发出的声音，一般用于纠正口误或鉴定音准。 | 互动直播、秀场直播、K 歌房等。                               | 免费                                                         |
| 自定义音频数据 | 支持自己采集音频回调，开发者可以对原始数据进行处理，进行自定义操作，例如外接非标设备、音频文件等。 | 非标设备接入、自定义音频效果、语音处理、语音识别等。         | 免费                                                         |
| 自定义视频数据 | 支持自定义的视频源和渲染器，使用非摄像头的视频源，例如视频文件、外接设备、第三方定制数据源等。 | 自定义美颜、定制数据源、多设备管理、视频识别、图像处理等。   | 免费                                                         |
| SEI 信息       | 通过 SEI 帧嵌入自定义信息到视频流中，同步给其他用户，例如歌词、题目等。 | K 歌房、答题直播、互动直播等。                               | 免费                                                         |


## 扩展功能

>?扩展功能是腾讯实时音视频产品结合腾讯云的其他云产品一起为您提供的增值服务，将由其他云产品根据各自的计费规则分别收取相关费用。


| 功能         | 功能说明                                                     | 常见应用场景                                       | 计费说明                                                     |
| ------------ | ------------------------------------------------------------ | -------------------------------------------------- | ------------------------------------------------------------ |
| CDN 直播观看 | 又称 “CDN 旁路直播”。TRTC 在云端使用旁路转码集群，将 TRTC 所使用的 UDP 协议转换为标准的直播 RTMP 协议，把 TRTC 的音视频数据推送到标准的云直播系统中，再经由 CDN 进行分发，从而实现 CDN 直播观看。 | 互动直播、直播分享、大型会议、直播远端观众观看等。 | 旁路直播属于增值服务，由 [云直播](https://intl.cloud.tencent.com/document/product/267) 收取相关费用，详情请参见 [CDN 直播观看 > 相关费用](https://intl.cloud.tencent.com/document/product/647/35242)。 |
| 即时通信 IM  | <ul style="margin:0"><li>可以通过 IM 的单聊、群聊及无人数上限的聊天室，实现聊天消息、评论、弹幕、送礼、点赞等功能。</li><li>可以通过 IM 进行信令交互，实现通话呼叫、房间用户数统计等功能。</li></ul> | 在线客服、互动直播、互动课堂、远程培训等。         | 即时通信 IM 属于增值服务，由 [即时通信 IM](https://intl.cloud.tencent.com/document/product/1047) 收取相关费用，详情请参见 [即时通信 IM 相关费用](https://intl.cloud.tencent.com/document/product/1047/34350)。 |
| AI 美颜      | 提供基于人脸识别技术的 AI 美颜、美妆、微整形、绿幕等各类型多种特效。 | 视频通话、互动直播、秀场直播等。                   | AI 美颜属于增值服务，由 美颜特效 SDK 收取相关费用。 |
| 语音内容审核 | 语音鉴黄、涉政等内容安全检测，可用于业务内容安全检查。       | 业务安全检查，合规等。                             | 语音内容审核属于增值服务，由**天御内容安全**收取相关费用，如需使用请 [联系我们](https://intl.cloud.tencent.com/contact-us) 申请开通。 |
| 视频内容审核 | 视频鉴黄、涉政等内容安全检测，可用于业务内容安全检查。       | 业务安全检查，合规等。                             | 视频内容审核属于增值服务，由 [云直播](https://intl.cloud.tencent.com/document/product/267) 收取相关费用，详情请参见 [智能鉴黄相关费用](https://intl.cloud.tencent.com/document/product/267/39607)。 |
