This document analyzes TRTC’s performance in terms of audio/video quality, latency, smoothness, stability, CPU usage, memory usage, battery consumption, heating, and other key indicators in tests under **normal** and **poor** network conditions and in **different application scenarios** (one-to-one, one-to-many, etc.).

## Performance Under Normal and Poor Network Conditions

### Scenario

Video call, interactive live streaming, and audio call

### Parameter configuration
- **Video call:**
<table><tr><th>Parameter</th><th>Value</th></tr>
<tr><td>Resolution</td><td>368 x 640</td></tr>
<tr><td>Bitrate</td><td>400 Kbps</td>
</tr><tr>
<td>Frame rate</td><td>15</td>
</tr></table>
- **Interactive live streaming:**
<table><tr><th>Parameter</th><th>Value</th></tr>
<tr><td>Resolution</td><td>720 x 1280</td></tr>
<tr>
<td>Bitrate</td><td>1200 Kbps</td>
</tr><tr>
<td>Frame rate</td><td>15</td>
</tr></table>



### Poor network tolerance test
The TRTC SDK was tested for its tolerance to different bad network conditions.
![](https://main.qcloudimg.com/raw/363a7f800bd4720c96cc8656a0eb6491.png)

>? For the metrics used to measure tolerance to poor network conditions, please see [Appendix 1: Network Metrics](#appendix1).

### Audio MOS under poor network conditions
TRTC can deliver relatively high-quality audio and low latency under poor network conditions.
The table below lists TRTC’s performance and mean opinion score (MOS) under different poor network conditions.
![](https://main.qcloudimg.com/raw/f7580010ffae2342bbba22967c9e514b.png)



## Client SDK Performance

### Tested devices
|  Device  |  Processor |   Memory  |
| ------------ | ----------- | ---- |
| Android device 1 | Qualcomm Snapdragon 835 - 8 cores | 6 GB   |
| Android device 2 | Kirin 980 - 8 cores | 8 GB   |
| iOS device 1     | Apple A8 - 2 cores      | 3 GB   |
| iOS device 2     | Apple A13 - 6 cores     | 4 GB   |

### Parameter configuration

| Parameter | Value |
| ------ | ------- |
| Resolution | 240 x 320 |
| Bitrate   | 100 Kbps |
| Frame rate   | 15      |

### Test scheme

- **Scenario**: one-to-one, one-to-two, one-to-three, one-to-four, one-to-eight
- **Duration**: 30 min for each scenario
- **Method**: a Linux robot is used to simulate streaming in one-to-many scenarios. Each device is tested independently.

### Test result

The TRTC SDK performs well in terms of CPU usage, memory usage, heating, and battery consumption. It uses a small amount of hardware resources but provides quality audio/video services.

- **App CPU usage:**
![](https://main.qcloudimg.com/raw/de4f28684d93db2964e4a97b6dcc9f7a.png)
- **App memory usage:**
![](https://main.qcloudimg.com/raw/a30a5ad382d3870db62a18c255dafc28.png)
- **System CPU usage**
![](https://main.qcloudimg.com/raw/d2dfc3d66296a38753002dc0982da26b.png)
- **System memory usage**
![](https://main.qcloudimg.com/raw/f9446367302bf4d7afa14e2cbab7c64d.png)
- **Battery drain after 30 min:**
![](https://main.qcloudimg.com/raw/a9f18fae1440d7eaafc97adabc2ba888.png)
- **Heat increase after 30 min:**
![](https://main.qcloudimg.com/raw/33b73b2194ef0cae9aba51b2e52f21b8.png)


[](id:appendix1)
## Appendix 1: Network Metrics

<table>
<tr><th width="17%">Metric</th><th width="50%">Description</th><th>Example</th>
</tr><tr>
<td>Loss</td>
<td>Packet loss rate</td>
<td>50%: for every 10 packets sent, 5 are lost.</td>
</tr><tr>
<td>Delay</td>
<td>Network delay</td>
<td>200: Data packets are delivered by the network 200 ms after they are sent by the SDK.</td>
</tr><tr>
<td>Jitter</td>
<td>Network jitter</td>
<td>300: Packet sending may be delayed 20 ms, 50 ms, 250 ms, 280 ms, or any value up to 300 ms. The average delay is 150 ms.</td>
</tr></table>

[](id:appendix2)
## Appendix 2: Performance Metrics Under Poor Network Conditions
<table>
<tr><th width="17%">Performance Metric</th><th width="50%">Description</th>
</tr><tr>
<td>MOS</td>
<td>An important measure of the audio quality of telecommunication systems. MOS is generated by Spirent Nomad using the POLQA standard. The higher the score, the higher the audio quality.</td>
</tr><tr>
<td>End-to-end latency</td>
<td>The time from when audio is captured at the sender end to when it is played back at the recipient end</td>
</tr><tr>
<td>Poor network tolerance test</td>
<td>Spirent Nomad is used to score the SDK under different poor network conditions using the <a href="#POLQA">POLQA</a> standard. Foreman video sequences are used to send data, and frame intervals are monitored at the recipient end. Data is collected at 30 points over a course of 10 min or longer. If there are <strong>perceptible abnormalities of 3 min at more than 3 data points</strong>, or <strong>the SDK is unavailable for a relatively long period of time</strong>, the SDK is considered intolerant of the network conditions.</td>
</tr></table>

>! Perceptual Objective Listening Quality Analysis (POLQA) is the ITU-T P.863 standard. It is a globally applicable standard used to score speech quality under different network conditions.[](id:POLQA)


[](id:appendix3)
## Appendix 3: SDK Performance Indicators

<table>
<tr><th width="16%">Indicator</th><th colspan=2>Description</th>
</tr><tr>
<td rowspan=2>App CPU usage</td>
<td>Android</td>
<td>Non-normalized CPU usage of the app, which is the same as the results generated by Android Studio Profiler</td>
</tr><tr>
<td>iOS</td>
<td>CPU usage of the app, which is the same as the results generated by Xcode<br><code>PerfDog usage = Xcode usage / Number of cores</code></td>
</tr><tr>
<td rowspan=2>System CPU usage</td>
<td>Android</td>
<td>Non-normalized CPU usage of the device, which is the same as the results generated by Android Studio Profiler</td>
</tr><tr>
<td>iOS</td>
<td>CPU usage of the device, which is the same as the results generated by Xcode<br><code>PerfDog usage = Xcode usage / number of cores</code></td>
</tr><tr>
<td rowspan=2>Memory usage</td>
<td>Android</td>
<td>Proportional set size (PSS), which is the same as the results generated by Android Java API and Meminfo</td>
</tr><tr>
<td>iOS</td>
<td>Xcode memory, which is obtained via debug gauges</td>
</tr><tr>
<td>Battery drain</td>
<td colspan=2>Decrease in battery percentage after 30 min (calculation starts the moment the battery percentage drops from 100% to 99%.)</td>
</tr><tr>
<td>Heat increase</td>
<td colspan=2>Temperature is measured with a thermometer when the app is not launched. Then run the app for 30 min under different scenarios. <br><code>Heat increase = Temperature after 30 min – Temperature when the app is not launched</code></td>
</tr></table>
