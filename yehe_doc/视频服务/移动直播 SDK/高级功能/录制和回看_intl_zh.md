## 功能介绍
录制回看是指您可以把用户整个直播过程录制下来，然后作为点播视频用于回看。

在 App 上线的初期阶段，由于主播数量比较少，所以在直播列表中加入录制回看，能够在一定程度上丰富 App 在观众端的信息量。即使到 App 成长起来主播数量形成规模以后，好的直播内容的沉淀依然是必不可少的一个部分，每个主播的个人介绍里除了有名字、照片和个人信息，历史直播的视频回看更是不可或缺的一个重要组成部分。

## 开启录制
录制回看功能依托于腾讯云的**云点播服务**支撑，如果您想要对接这个功能，首先需要在腾讯云的管理控制台 [开通云点播服务](https://console.cloud.tencent.com/vod)。服务开通之后，新录制的文件就可以在云点播控制台的 [视频管理](http://console.cloud.tencent.com/vod/media) 里找到它们。

开启录制的方法如下：
>? 
>- 如需通过 API 对直播频道进行录制，详细请参见 [创建录制任务](https://intl.cloud.tencent.com/document/product/267/37309)。
>- 录制转点播后，文件自动存放于点播平台，故用户需在使用录制功能前，提前开通点播服务并购买相关空间和流量用于存放和播放录制后的视频文件，详细请参见 [点播快速入门](https://intl.cloud.tencent.com/document/product/266/8757)。

#### 基本步骤
在云直播控制台菜单栏内选择【功能配置】>【[直播录制](https://console.cloud.tencent.com/live/config/record)】，单击【创建录制模板】进行设置。设置完基本信息后，单击【保存】。具体操作请参见 [录制模板配置](https://intl.cloud.tencent.com/document/product/267/34223)。
**规格说明：**

1. 录制视频针对直播原始码率录制，输出格式有 HLS、MP4、FLV 和 AAC 四种，其中 AAC 为纯音频录制。
2. 录制 MP4、FLV 或 AAC 格式单个文件时长限制为1分钟 - 120分钟。
3. 录制 HLS 格式最长单个文件时长无限制，如果超出续录超时时间则新建文件继续录制。
4. 单个录制文件保存最大时长均为1500天。
5. 仅 HLS 格式支持文件推流中断续录，续录超时时长可设置为0s - 1800s。
6. 直播过程中预计在录制结束5分钟左右可获取对应文件。例如，某直播从12:00开始录制，12:30结束录制，则12:35左右可获取12:00 - 12:30的对应片段。
7. 受限于音视频文件格式（FLV/MP4/HLS）对编码类型的支持，视频编码类型支持 H.264，音频编码类型支持 AAC。

#### 关联域名
创建好录制模板后，需在【[域名管理](https://console.cloud.tencent.com/live/domainmanage)】中，选择对应的推流域名，进入【模板配置】栏，单击【录制配置】>【编辑】为该域名指定录制模板后，单击【保存】即可。更多详情请参见 [关联录制模板](https://intl.cloud.tencent.com/document/product/267/34224)。

## 获取文件
一个新的录制视频文件生成后，会相应的生成一个观看地址，您可以按照自己的业务需求对其进行处理。

您可以结合自己的业务场景实现很多的扩展功能，例如：您可以将其追加到主播的资料信息里，作为该主播曾经直播的节目而存在；或者将其放入回放列表中，经过专门的人工筛选，将优质的视频推荐给您的 App 用户。

如何才能拿到文件的地址，有如下两种解决方案：

### 方案1：被动监听通知
您可以使用腾讯云的 **[回调配置](https://intl.cloud.tencent.com/document/product/267/31074)**：您的服务器注册一个自己的**回调 URL** 给腾讯云，腾讯云会在一个新的录制文件生成时通过这个 URL 通知给您。

在云直播菜单栏内选择【事件中心】>【[直播回调](https://console.cloud.tencent.com/live/config/callback)】，单击【创建回调模板】。在回调设置弹框中填写完成回调信息，单击【保存】即可。更多详情请参见 [创建回调模板](https://intl.cloud.tencent.com/document/product/267/31074#Callback)。

**关联域名**
创建好回调模板后，需通在【[域名管理](https://console.cloud.tencent.com/live/domainmanage)】中，选择对应的推流域名，进入【模板配置】栏，单击【回调配置】>【编辑】为该域名指定回调模板后，单击【保存】即可。

如下是一个典型的通知消息，它的含义是：一个 ID 为`9192487266581821586`的新的 FLV 录制文件已经生成，播放地址为：`http://200025724.vod.myqcloud.com/200025724_ac92b781a22c4a3e937c9e61c2624af7.f0.flv`。

```json
{
    "channel_id": "2121_15919131751",
    "end_time": 1473125627,
    "event_type": 100,
    "file_format": "flv",
    "file_id": "9192487266581821586",
    "file_size": 9749353,
    "sign": "fef79a097458ed80b5f5574cbc13e1fd",
    "start_time": 1473135647,
    "stream_id": "2121_15919131751",
    "t": 1473126233,
    "video_id": "200025724_ac92b781a22c4a3e937c9e61c2624af7",
    "video_url": "http://200025724.vod.myqcloud.com/200025724_ac92b781a22c4a3e937c9e61c2624af7.f0.flv"
}
```

### 方案2：主动查询获取
录制文件生成后自动存储到点播系统，您可以直接在点播系统查看，或直接通过点播 API 查询，详情请参见 [录制文件获取](https://intl.cloud.tencent.com/document/product/267/31563) 。

## 常见问题
[](id:que1)
### 1. 直播录制的原理是什么？
![](https://main.qcloudimg.com/raw/334a262df93cd5eafcca740033894446.png)
对于一条直播流，一旦开启录制，音视频数据就会被旁路到录制系统。主播的手机推上来的每一帧数据，都会被录制系统追加写入到录制文件中。

一旦直播流中断，接入层会立刻通知录制服务器将正在写入的文件落地，将其转存到点播系统中，并为其生成索引，这样您在点播系统中就会看到这个新生成的录制文件了。同时，如果您配置了录制事件通知，录制系统会将该文件的**索引 ID** 和**在线播放地址**等信息通知给您之前配置的服务器上。

但是，如果一个文件过大，在云端的转出和处理过程中就很容易出错，所以为了确保成功率，我们的单个录制文件最长不会超过120分钟，您可以通过 RecordInterval 参数指定更短的分片。

[](id:que2)
### 2. 一次直播会有几个录制文件？
- **录制 MP4、FLV 或 AAC 格式**：单个文件时长限制为1分钟 - 120分钟。您可以通过 [创建录制模板](https://intl.cloud.tencent.com/document/product/267/30845) 接口中的 RecordInterval 参数指定更短的分片。
  - 如果一次直播过程非常短暂，录制模块未启动就结束推流，那么系统会无法生成录制文件。
  - 如果一次直播时间不算长（小于 RecordInterval），且中途没有推流中断的事情发生，那么通常只有一个文件。
  - 如果一次直播时间很长（超过 RecordInterval ），那么会按照 RecordInterval 指定的时间长度进行分片，分片的原因是避免过长的文件在分布式系统中流转时间的不确定性。
  - 如果一次直播过程中发生推流中断（之后 SDK 会尝试重新推流），那么每次中断均会产生一个新的分片。
- **录制 HLS 格式**：最长单个文件时长无限制，如果超出续录超时时间则新建文件继续录制。续录超时时长可设置为0s - 1800s。

[](id:que3)
### 3. 如何知道哪些文件属于某一次直播？
准确来说，作为 PAAS 的腾讯云并不清楚您的一次直播是怎么定义的，如果您的一次直播持续了20分钟，但中间有一次因为网络切换导致的断流，以及一次手动的停止和重启，那么这算是一次直播还是三次呢？

对于普通的移动直播场景，我们一般定义如下的界面之间的这段时间为一次直播：
![](https://main.qcloudimg.com/raw/e91b79fed8b397a4fc7e67bd9b302d1a.png)

所以来自 App 客户端的时间信息很重要，如果您希望定义这段时间内的录制文件都属于这次直播，那么只需要用直播码和时间信息检索收到的录制通知即可（每一条录制通知事件都会携带 StreamID、开始时间和结束时间等信息）。

[](id:que4)
### 4. 如何把碎片拼接起来？
目前腾讯云支持使用云端 API 接口拼接视频分片。
