## PushEvent

### 常规事件 

每一次成功的推流都会有通知事件，例如收到1003就意味着摄像头的画面开始渲染。

| code                 |    事件定义  |  含义说明                    |
| -------------------  | -------- |  ------------------------ |
| 1001 | PUSH_EVT_CONNECT_SUCC | 已经成功连接到云端服务器 |
| 1002 | PUSH_EVT_PUSH_BEGIN       | 与服务器握手完毕，一切正常，准备开始上行推流 |
| 1003 | PUSH_EVT_OPEN_CAMERA_SUCC  |  已成功启动摄像头，摄像头被占用或者被限制权限的情况下无法打开 |
| 1004 | PUSH_EVT_SCREEN_CAPTURE_SUCC  |  录屏启动成功 （Android SDK 专用） |
| 1005 | PUSH_EVT_CHANGE_RESOLUTION | 推流动态调整分辨率 |
| 1006 | PUSH_EVT_CHANGE_BITRATE | 推流动态调整码率 |
| 1007 | PUSH_EVT_FIRST_FRAME_AVAILABLE | 首帧画面采集完成 |
| 1008 | PUSH_EVT_START_VIDEO_ENCODER | 编码器启动 |
| 1009 | PUSH_EVT_CAMERA_REMOVED | 摄像头设备已被移出（Windows SDK 专用） |
| 1010 | PUSH_EVT_CAMERA_AVAILABLE | 摄像头设备重新可用（Windows SDK 专用） |
| 1011 | PUSH_EVT_CAMERA_CLOSED | 关闭摄像头完成（Windows SDK 专用） |
| 1012 | PUSH_EVT_SNAPSHOT_RESULT | 截图快照返回码（Windows SDK 专用） |
| 1018 | PUSH_EVT_ROOM_IN | 已经在 webrtc 房间里面，进房成功后通知 |
| 1019 | PUSH_EVT_ROOM_OUT | 不在 webrtc 房间里面，进房失败或者中途退出房间时通知 |
| 1020 | PUSH_EVT_ROOM_USERLIST | 下发 webrtc 房间成员列表（不包括自己）|
| 1021 | PUSH_EVT_ROOM_NEED_REENTER | Wi-Fi 切换到 4G 会触发断线重连，此时需要重新进入 webrtc 房间（拉取最优的服务器地址）|

### 严重错误

SDK 发现了一些严重问题，推流无法继续了，例如用户禁用了 App 的 Camera 权限导致摄像头打不开。

>!视频编码失败并不会直接影响推流，SDK 会做自行处理以保证后面的视频编码成功。


| code | 事件定义 | 含义说明 |
| --- | --- | --- |
| -1301 | PUSH_ERR_OPEN_CAMERA_FAIL | 打开摄像头失败 |
| -1302 | PUSH_ERR_OPEN_MIC_FAIL | 	打开麦克风失败 |
| -1303 | PUSH_ERR_VIDEO_ENCODE_FAIL | 	视频编码失败 |
| -1304 | PUSH_ERR_AUDIO_ENCODE_FAIL | 音频编码失败 |
| -1305 | PUSH_ERR_UNSUPPORTED_RESOLUTION | 不支持的视频分辨率 |
| -1306 | PUSH_ERR_UNSUPPORTED_SAMPLERATE | 不支持的音频采样率 |
| -1307 | PUSH_ERR_NET_DISCONNECT | 网络断连，且连续三次无法重新连接，需要自行重启推流 |
| -1308 | PUSH_ERR_CAMERA_OCCUPY<br>PUSH_ERR_AUDIO_SYSTEM_NOT_WORK<br>PUSH_ERR_SCREEN_CAPTURE_START_FAILED | 摄像头正在被占用中，可尝试打开其他摄像头（Windows）<br>系统异常，录音失败（iOS）<br>开始录屏失败，可能是被用户拒绝了（Android） |
| -1309 | PUSH_ERR_SCREEN_CAPTURE_UNSURPORT | 录屏失败，不支持的 Android 系统版本，需要5.0以上的系统（Android SDK 专用） |

### 警告事件 

大部分的警告事件会触发一些重试性的保护逻辑或者恢复逻辑，很大概率能够由 SDK 自行恢复。部分警告事件需要由开发者处理。

- **WARNING_NET_BUSY：**主播网络不给力，可以通过 UI 向用户进行提示。

- **WARNING_SERVER_DISCONNECT：**推流请求被后台拒绝了，出现这个问题一般是由于推流地址里的 txSecret 计算错了，或者是推流地址被其他人占用了（一个推流 URL 同时只能有一个端推流）。

| code                 |    事件定义  |  含义说明                    |
| -------------------  | -------- |  -----------------------|
| 1101 | PUSH_WARNING_NET_BUSY             | 上行网速不够用，建议提示用户改善当前的网络环境|
| 1102 | PUSH_WARNING_RECONNECT           | 网络断连，已启动重连流程（重试失败超过三次会放弃）|
| 1103 | PUSH_WARNING_HW_ACCELERATION_FAIL| 硬编码启动失败，自动切换到软编码|
| 1104 | PUSH_WARNING_VIDEO_ENCODE_FAIL | 视频编码失败，非致命错，内部会重启编码器            |
| 1107 | PUSH_WARNING_VIDEO_ENCODE_SW_SWITCH_HW     |  由于机器性能问题，自动切换到硬件编码（Android SDK 专用）|
| 3001 | PUSH_WARNING_DNS_FAIL                |  DNS 解析失败，启动重试流程     |
| 3002 | PUSH_WARNING_SEVER_CONN_FAIL |  服务器连接失败，启动重试流程  |
| 3003 | PUSH_WARNING_SHAKE_FAIL            |  服务器握手失败，启动重试流程  |
| 3004 | PUSH_WARNING_SERVER_DISCONNECT   |  RTMP 服务器主动断开，请检查推流地址的合法性或防盗链有效期 |
| 3005 | PUSH_WARNING_READ_WRITE_FAIL   |  RTMP 读/写失败，将会断开连接 |


## PlayEvent

### 关键事件

| code | 事件定义 | 含义说明 |
| --- | --- | --- |
| 2001 | PLAY_EVT_CONNECT_SUCC | 已经连接服务器 |
| 2002 | PLAY_EVT_RTMP_STREAM_BEGIN | 已经连接服务器，开始拉流 |
| 2003 | PLAY_EVT_RCV_FIRST_I_FRAME | 	渲染首个视频数据包（IDR）|
| 2004 | PLAY_EVT_PLAY_BEGIN | 视频播放开始 |
| 2005 | PLAY_EVT_PLAY_PROGRESS | 视频播放进度（点播专用）|
| 2006 | PLAY_EVT_PLAY_END | 视频播放结束 |
| 2007 | PLAY_EVT_PLAY_LOADING | 视频播放加载中 |
| 2008 | PLAY_EVT_START_VIDEO_DECODER | 解码器启动 |
| 2009 | PLAY_EVT_CHANGE_RESOLUTION | 	视频分辨率改变 |
| 2010 | PLAY_EVT_GET_PLAYINFO_SUCC<br>PLAY_EVT_SNAPSHOT_RESULT | 	获取点播文件信息成功（Android iOS）<br>系截图快照返回码（Windows） |
| 2011 | PLAY_EVT_CHANGE_ROTATION | MP4 视频旋转角度（Android、 iOS） |
| 2012 | PLAY_EVT_GET_MESSAGE | 用于接收夹在音视频流中的消息 |
| 2013 | PLAY_EVT_PREPARED | 视频加载完毕（Android、 iOS） |
| 2014 | PLAY_EVT_VOD_LOADING_END | 加载结束（Android、 iOS） |
| -2301 | PLAY_ERR_NET_DISCONNECT | 网络断连，且连续三次无法重新连接，需要自行重启推流 |
| -2302 | PLAY_ERR_GET_RTMP_ACC_URL_FAIL | 	获取加速拉流失败，这是由于您传给`liveplayer`的加速流地址中没有携带`txTime`和`txSecret`签名，或者是签名计算的不对。出现这个错误时，`liveplayer`会放弃拉取加速流转而拉取 CDN 上的视频流，从而导致延迟很大。<br>需要注意：只有 RTMP 协议的播放地址才支持低延时加速。 |
| -2303 | PLAY_ERR_FILE_NOT_FOUND | 播放文件不存在（Android、 iOS） |
| -2304 | PLAY_ERR_HEVC_DECODE_FAIL | 	H265 解码失败（Android、 iOS） |
| -2305 | PLAY_ERR_HLS_KEY | 	HLS 解码 key 获取失败（Android、 iOS） |
| -2306 | PLAY_ERR_GET_PLAYINFO_FAIL | 	获取点播文件信息失败（Android、 iOS） |

>! 
>- **判断直播是否结束：**基于各种标准的实现原理不同，很多直播流通常没有结束事件（2006）抛出，此时可预期的表现是：主播结束推流后，SDK 会很快发现数据流拉取失败（WARNING_RECONNECT），然后开始重试，直至三次重试失败后抛出 PLAY_ERR_NET_DISCONNECT 事件。所以2006和 -2301都要判断，用来作为直播结束的判定事件。
>- **不要在收到 PLAY_LOADING 后隐藏播放画面：**因为 PLAY_LOADING 到 PLAY_BEGIN 的时间长短是不确定的，可能是5s也可能是5ms，有些客户考虑在 LOADING 时隐藏画面， BEGIN 时显示画面，会造成严重的画面闪烁（尤其是直播场景下）。推荐的做法是在视频播放画面上叠加一个半透明的加载动画。

### 警告事件

内部警告并非不可恢复的错误，SDK 会启动相应的恢复措施，警告的目的主要用于提示开发者或者最终用户。

| code                 |    事件定义  |  含义说明           |
| -------------------  | -------- |  ------------------------ |
| 2101 | PLAY_WARNING_VIDEO_DECODE_FAIL   |   当前视频帧解码失败  |
| 2102 | PLAY_WARNING_AUDIO_DECODE_FAIL  |   当前音频帧解码失败  |
| 2103 | PLAY_WARNING_RECONNECT   | 网络断连，已启动自动重连恢复（重连超过三次就直接抛送 PLAY_ERR_NET_DISCONNECT 了）|
| 2104 | PLAY_WARNING_RECV_DATA_LAG        | 视频流不太稳定，可能是观看者当前网速不充裕 |
| 2105 | PLAY_WARNING_VIDEO_PLAY_LAG       | 当前视频播放出现卡顿|
| 2106 | PLAY_WARNING_HW_ACCELERATION_FAIL  | 硬解启动失败，采用软解   |
| 2107 | PLAY_WARNING_VIDEO_DISCONTINUITY   | 当前视频帧不连续，视频源可能有丢帧，可能会导致画面花屏 |
| 2108 | PLAY_WARNING_FIRST_IDR_HW_DECODE_FAIL | 当前流硬解第一个 I 帧失败，SDK 自动切软解           |
| 3001 | PLAY_WARNING_DNS_FAIL                 | DNS 解析失败（仅播放 RTMP:// 地址时会抛送）|
| 3002 | PLAY_WARNING_SEVER_CONN_FAIL  | 服务器连接失败（仅播放 RTMP:// 地址时会抛送）|
| 3003 | PLAY_WARNING_SHAKE_FAIL             | 服务器握手失败（仅播放 RTMP:// 地址时会抛送）|
| 3004 | PLAY_WARNING_SERVER_DISCONNECT | RTMP 服务器主动断开                     |
   
