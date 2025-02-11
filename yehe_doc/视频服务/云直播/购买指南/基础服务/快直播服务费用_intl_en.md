## Notes

- Billing mode: **daily pay-as-you-go mode**
- Billing cycle: daily billing cycle. Traffic fees generated in one day will be deducted the next day. See your billing statement for the actual bill generation time and amount.
- The conversion scale for traffic/bandwidth is 1,000. For example, 1 TB = 1,000 GB.
- A CSS service day is 00:00-23:59 (UTC+8).
- As LEB uses channels with ultra-low latency, its traffic/bandwidth fees are a bit higher than those of LVB.
- LEB does not support playing back live streams with B-frames. If the pushed stream contains B-frames, the system will remove them by transcoding, which will incur transcoding fees.
- Pull by web browser only supports the standard WebRTC protocol and does not support the AAC audio codec. To push streams with audios in AAC format, the audios will be transcoded into Opus format, which will incur audio transcoding fees.
- Starting from 00:00 on January 4, 2022, CSS will adjust the daily billing prices and pricing tiers of the basic services of LEB and will bill usage outside the Chinese mainland by region instead of at a unified price. For details, see [Notice: CSS to Adjust Prices of Basic Services]( https://intl.cloud.tencent.com/document/product/267/43055).

>! 
>- By default, LEB fees are billed by downstream usage. However, upstream usage will also be billed when the ratio of upstream usage and downstream usage is larger than 1:10 and the daily upstream peak bandwidth exceeds 100 Mbps.
> - **The same billing method, tiered pricing rules, and billing regions (in/outside the Chinese mainland)** are used for live push and [LVB playback](https://intl.cloud.tencent.com/document/product/267/2818). Live push has been billed since 00:00 (UTC+08:00), July 1, 2021.
>- Billing example:
Take daily bill-by-traffic for example. Suppose the upstream traffic usage of an LEB session in one day is 10 GB, the downstream traffic usage is 90 GB, and the daily upstream peak bandwidth is 101 Mbps. As the ratio of upstream usage to downstream usage = 10:90 > 1:10 and the daily upstream peak bandwidth > 100 Mbps, the traffic fees would be as follows:
Daily traffic fees = Upstream traffic fees + Downstream traffic fees = 0.0417 (USD/GB/Day) x (10 (GB) + 90 (GB)) = 4.17 USD.



[](id:overseas)
## Global Acceleration

LEB displays the usage of downstream traffic and bandwidth generated when connecting users and global acceleration origin servers. LEB provides two daily pay-as-you-go billing modes: [bill-by-traffic](#overseas_flow) and [bill-by-bandwidth](#overseas_bandwidth). The default billing mode for new users is bill-by-traffic.

>! LEB bill-by-traffic/bandwidth rules for regions outside Chinese mainland took effect on April 20, 2021. Since April 21, 2021, all bills have been generated according to the new billing rules.**

[](id:overseas_flow)
### Global bill-by-traffic

#### Pricing
Global LEB bill-by-traffic utilizes tiered pricing with a daily billing cycle, as detailed in the table below:

| Traffic Tier | Price (USD/GB/Day) |
| ----------------- | ---------------- |
| 0 - 500 GB         | 0.1445           |
| 500 GB (inclusive) - 2 TB  | 0.1371    |
| 2 TB (inclusive) - 50 TB   | 0.1307      |
| 50 TB (inclusive) - 100 TB | 0.1240     |
| ≥ 100 TB           | 0.1097           |

#### Billing
- Billable item: the downstream traffic generated by LEB video streams outside the Chinese mainland.
- Billing rules: the fees are calculated by multiplying the accumulated traffic on a day and the unit price in the corresponding tier.

#### Billing example
- Suppose an LEB session lasts for 1 hour at a bitrate of 500 Kbps, which is the sum of the audio bitrate and the video bitrate. If you enable transcoding and specify a video bitrate, the sum of the audio bitrate and the specified video bitrate will be used for billing. If there are 100 viewers, the consumed bandwidth will be approximately: 500/8 x 3600 x 100 = 22,500,000 KB = 22.5 GB.
- If you held a global LEB session that generated 22.5 GB of downstream traffic on April 1, 2021, then the LEB traffic fees you would need to pay on April 2, 2021 would be as follows:
  Daily LEB traffic fees = 0.1445 (USD/GB) × 22.5 (GB) = 3.25125 USD.
-  By default, fees are billed by downstream usage. However, upstream usage will also be billed when the ratio of upstream usage and downstream usage is larger than 1:10, and the daily upstream peak bandwidth exceeds 100 Mbps. Upstream usage will be billed according to the same billing modes and tiered pricing rules as LVB downstream usage.

[](id:overseas_bandwidth)
### Global bill-by-bandwidth

#### Pricing

Global LEB bill-by-bandwidth utilizes tiered pricing by the daily peak bandwidth with a daily billing cycle, as detailed in the table below:

| Bandwidth Tier | Price (USD/Mbps/Day) |
| -------------------- | ------------------ |
| 0 - 500 Mbps          | 0.4194             |
| 500 Mbps (inclusive) - 5 Gbps | 0.3871             |
| ≥ 5 Gbps              | 0.3540              |

#### Billing
- Billable item: the downstream bandwidth generated by LEB video streams outside the Chinese mainland.
- Billing rules: the fees are calculated by multiplying the peak bandwidth on a day and the unit price in the corresponding tier.

#### Billing example
- Suppose a LEB session lasts for 1 hour at a bitrate of 500 Kbps, which is the sum of the audio bitrate and the video bitrate. If you enable transcoding and specify a video bitrate, the sum of the audio bitrate and the specified video bitrate will be used for billing. If there are 100 viewers, the consumed bandwidth will be approximately:
   500 Kbps x 100 = 50,000 Kbps = 50 Mbps.
- If you held a global LEB session that generated 50 Mbps of downstream bandwidth on April 1, 2021, then the LEB bandwidth fees you would need to pay on April 2, 2021 would be as follows:
   Daily LEB bandwidth fees = 0.4194 (USD/Mbps/Day) × 50 (Mbps) = 20.97 USD.
-  By default, fees are billed by downstream usage. However, upstream usage will also be billed when the ratio of upstream usage and downstream usage is larger than 1:10, and the daily upstream peak bandwidth exceeds 100 Mbps. Upstream usage will be billed according to the same billing modes and tiered pricing rules as LVB downstream usage.

[](id:domestic)

## Bill-by-Traffic/Bandwidth

The LEB service is billed by downstream traffic/bandwidth generated during live streaming.
LEB provides two daily pay-as-you-go billing modes: [bill-by-traffic](#flow) and [bill-by-bandwidth](#bandwidth). You can choose the billing mode that best suits your needs. **The default mode for new users of LEB is bill-by-traffic.**

[](id:flow)

### Bill-by-traffic

#### Pricing

LEB bill-by-traffic utilizes tiered pricing with a daily billing cycle, as detailed in the table below:

| Traffic Tier | Price (USD/GB/Day) |
| ----------------- | ---------------- |
| 0 - 500 GB         | 0.0835           |
| 500 GB (inclusive) - 2 TB  | 0.0797           |
| 2 TB (inclusive) - 50 TB   | 0.0733           |
| 50 TB (inclusive) - 100 TB | 0.0620           |
| ≥ 100 TB           | 0.0516           |

#### Billing

- Billable item: the downstream traffic generated by LEB video streams in the Chinese mainland.
- Billing rules: the fees are calculated by multiplying the accumulated traffic on a day and the unit price in the corresponding tier.

#### Billing example

- Suppose an LEB session lasts for 1 hour at a bitrate of 500 Kbps, which is the sum of the audio bitrate and the video bitrate. If you enable transcoding and specify a video bitrate, the sum of the audio bitrate and the specified video bitrate will be used for billing. If there are 100 viewers, the consumed bandwidth will be approximately: 500/8 x 3600 x 100 = 22,500,000 KB = 22.5 GB.
- Suppose this LEB session was held on October 1, 2020. The traffic fees you need to pay on October 2, 2020 are as follows:
  Daily LEB traffic fees = 0.0835 (USD/GB) × 22.5 (GB) = 1.87875 USD.
-  By default, fees are billed by downstream usage. However, upstream usage will also be billed when the ratio of upstream usage and downstream usage is larger than 1:10, and the daily upstream peak bandwidth exceeds 100 Mbps. Upstream usage will be billed according to the same billing modes and tiered pricing rules as LVB downstream usage.

[](id:bandwidth)

### Bill-by-bandwidth

#### Pricing

LEB bill-by-bandwidth utilizes tiered pricing by the daily peak bandwidth with a daily billing cycle, as detailed in the table below:

| Bandwidth Tier | Price (USD/Mbps/Day) |
| -------------------- | ------------------ |
| 0 - 500 Mbps          | 0.2065             |
| 500 Mbps (inclusive) - 5 Gbps | 0.2000             |
| 5 Gbps (inclusive) - 20 Gbps  | 0.1903             |
| ≥ 20 Gbps             | 0.1871             |

#### Billing

- Billable item: the downstream bandwidth generated by LEB video streams in the Chinese mainland.
- Billing rules: the fees are calculated by multiplying the peak bandwidth on a day and the unit price in the corresponding tier.

#### Billing example

- Suppose an LEB session lasts for 1 hour at a bitrate of 500 Kbps, which is the sum of the audio bitrate and the video bitrate. If you enable transcoding and specify a video bitrate, the sum of the audio bitrate and the specified video bitrate will be used for billing. If there are 100 viewers, the consumed bandwidth will be approximately:
   500 Kbps x 100 = 50,000 Kbps = 50 Mbps.
-  If you held an LEB session that generated 50 Mbps of downstream bandwidth on October 1, 2020, then the bandwidth fees you would need to pay on October 2, 2020 would be as follows:
   Daily LEB bandwidth fees = 0.2065 (USD/Mbps/Day) × 50 (Mbps) = 10.325 USD.
-  By default, fees are billed by downstream usage. However, upstream usage will also be billed when the ratio of upstream usage and downstream usage is larger than 1:10, and the daily upstream peak bandwidth exceeds 100 Mbps. Upstream usage will be billed according to the same billing modes and tiered pricing rules as LVB downstream usage.

>? If you have a large-scale live streaming business, then a daily billing mode may not meet your needs. Please contact Tencent Cloud sales or [submit a ticket](https://console.cloud.tencent.com/workorder/category) to determine the best billing mode for you.