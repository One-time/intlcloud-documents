消息队列 CKafka 实例按照规格分为标准版和专业版，两个版本的对比如下：


| 项目                              | 专业版                                                       | 标准版                                                       |
| --------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 版本                              | <li>兼容开源0.9、0.10、1.1、2.4、2.8版本</li><li>可以在购买时自由选择</li> | <li>兼容开源0.9、0.10、1.1版本</li><li>默认安装1.1版本，不支持定制版本</li> |
| 实例类型                          | 专享实例             | 共享物理节点资源                                             |
| 稳定性 SLA                        | 99.995%                                                      | 99.95%                                                       |
| 带宽规格范围                     | 最高10000MB/s，详情参考 [计费概述](https://intl.cloud.tencent.com/document/product/597/11745)         | 最高150MB/s，详情参考 [计费概述](https://intl.cloud.tencent.com/document/product/597/11745)          |
| <nobr>Topic/Partition 规格</nobr> | <li>相同带宽下 Topic/Partition 容量远大于标准版</li> <li>支持在一定范围内额外购买 Partition 包来扩容上限</li> | 每个型号固定上限                                             |
| 扩容                              | 自由度高，可以单独扩容带宽、Topic/Partition上限、磁盘        | 自由度一般，可以单独扩容磁盘                                 |
| 自动化清理磁盘                    | 是，自动清理过期数据                                         | 否，磁盘满后需要 [提交工单](https://console.cloud.tencent.com/workorder/category?level1_id=876&level2_id=951&source=0&data_title=%E6%B6%88%E6%81%AF%E9%98%9F%E5%88%97%20CKafka&level3_id=955&radio_title=%E9%85%8D%E9%A2%9D%E6%8F%90%E5%8D%87%E7%94%B3%E8%AF%B7&queue=81&scene_code=18356&step=2) 处理 |
| broker 修复升级周期                   | 快速升级           | 共享集群，周期较长                         |
| 高可用能力                        | 支持同地域自定义多可用区部署，提升容灾能力                   | 不支持同城跨可用区部署，依赖于后台迁移，需要 [提交工单](https://console.cloud.tencent.com/workorder/category?level1_id=876&level2_id=951&source=0&data_title=%E6%B6%88%E6%81%AF%E9%98%9F%E5%88%97%20CKafka&level3_id=954&radio_title=%E4%BD%BF%E7%94%A8%E5%92%A8%E8%AF%A2(SDK/API/%E4%BA%A7%E5%93%81%E7%AD%89)&queue=81&scene_code=18346&step=2) 申请，一般处理周期为10个工作日 |
| 高级特性                          | <li>定时 rebalance，升配可以自定义 rebalance 执行时间，避开业务高峰，详情参见 [升配实例](https://intl.cloud.tencent.com/document/product/597/40650)</li><li>高级监控（包括网络稳定性分析，请求时延分析等），详情参见 [查询高级监控信息](https://intl.cloud.tencent.com/document/product/597/40038)</li><li>支持根据磁盘水位动态调节消息保留策略，详情参见 [添加消息动态保留策略](https://intl.cloud.tencent.com/document/product/597/40211)</li> | 无                                                           |
| 技术服务                          | 提供参数优化咨询服务，可以针对部分特殊的业务场景定制化参数配置，您可以 [提交工单](https://console.cloud.tencent.com/workorder/category?level1_id=876&level2_id=951&source=0&data_title=%E6%B6%88%E6%81%AF%E9%98%9F%E5%88%97%20CKafka&level3_id=954&radio_title=%E4%BD%BF%E7%94%A8%E5%92%A8%E8%AF%A2(SDK/API/%E4%BA%A7%E5%93%81%E7%AD%89)&queue=81&scene_code=18346&step=2) 申请 | 基础的故障处理和问题修复                                     |


>?**专业版**默认开启自动化清理磁盘功能，当实例磁盘满了以后，会自动清理最早数据，保证实例可用。
