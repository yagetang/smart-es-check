# README
本脚本调用es api 输出集群基本信息，方便及时获取集群的状态，便于诊断相关问题。
脚本纯shell编写，支持ubuntu和centos系统，如果有相关建议和bug反馈，欢迎告知，联系QQ：3452127307

## 使用方法

获取脚本，直接运行 

```
# sh es-check.sh
```

### 注意事项

1. 脚本请在linux环境下运行，确保这个linux网络能跟es集群的网络互通
2. 执行脚本建议使用超级用户elastic
3. 默认请求9200端口，若您的集群不是9200端口，请尝试把所有端口替换成您的端口


## 效果展示
```
[root@es_kibana_logstash /tmp]# sh es-check.sh 
# ------------------------------------------------------------------------------
# 您好！本脚本纯shell编写, 用于收集ES基础信息
#
# 脚本开源, 您可以用编辑器打开脚本查阅里面的代码。
#
# 确认脚本无误后, 放到ES集群节点上运行。
# ------------------------------------------------------------------------------

请输入es VIP地址（这个IP地址可以到控制台里查看到）：***
您输入的ES VIP是：10.113.12.20 您运行此脚本的本机IP地址是：*** 请再次确认它们是在同一VPC或者网络互通的情况下哦, 不然网络不可达脚本检测会失败
确认请输入(Y)退出请输入(N): Y/N：y
您的es服务有无设置您名密码安全认证？（也就是登录kibana的用户名密码） Y/N：y
请输入您的您的您名（建议用elastic超级用户执行，其他权限用户权限会存在不足获取信息不准情况）：elastic
请输入您的密码（我们不会记录您的密码）：****
集群智能分析中, 请稍后... 如果长时间卡住没弹出结果请按ctrl+C终止重试
--------------------------以下是智能分析结果----------------------------
当前集群的名字是：elk-cluster
执行脚本输入的您名：elastic
当前集群健康状态是：green
当前集群是否存在time_out: false
当前集群的节点数是：8
当前集群data node总数是：7
当前集群文档总数是：58,634,538
当前集群的总分片数是: 2005
当前集群的主分片数是: 1000
当前集群可用分片百分比是：100.0%
当前集群节点存储已使用(只统计data节点)：140 gb
当前集群存储还剩余空间(只统计data节点)：1236 gb
当前集群正在迁移的分片数：0
当前集群初始化的分片数：0
当前集群没有被分配到节点的分片数：0
当前集群在等待的任务数：0
当前集群number_of_in_flight_fetch：0
当前集群task_max_waiting_in_queue_millis：0
当前集群信息智能检测：
1. 当前总分片数除于节点数值为：286.42 , 没有整除, 这样会导致数据分片分布不均匀, 造成一定的数据热点问题，建议默认分片数设置为data node节点数的倍数。
2. 当前总分片数 > 1000, 分片数过大会一定的影响集群读写性能、内存不足等问题, 总分片数=index索引数*默认设置分片数*（副本数+1）, 如果分片数过大, 可以调整默认分片数设置或副本数设置。
3. 当前索引数大于100, 系统索引:709, 您自建索引（业务索引）:53, 如果您是日志场景请注意过期日志数据要定期删除, 索引的建立最好按周、按月或者按年的时间维度来创建, 按天索引数会很多。
4. 数据量大小排名前五的索引分别是：
 (1) access-2019, 它总大小是: 1945 mb, 它的默认分片设置number_of_shards=5, 副本数设置number_of_replicas=2,它每个分片大小目前为：1945 / (5 * (2 + 1) ) = 194 mb 
 (2) tss-2017, 它总大小是: 1430 mb, 它的默认分片设置number_of_shards=5, 副本数设置number_of_replicas=2,它每个分片大小目前为：1430 / (5 * (2 + 1) ) = 143 mb 
 (3) tss-2018, 它总大小是: 842 mb, 它的默认分片设置number_of_shards=5, 副本数设置number_of_replicas=2,它每个分片大小目前为：842 / (5 * (2 + 1) ) = 84 mb 
 (4) buy_vm-2018, 它总大小是: 590 mb, 它的默认分片设置number_of_shards=5, 副本数设置number_of_replicas=2,它每个分片大小目前为：590 / (5 * (2 + 1) ) = 59 mb 
 (5) tss-2019, 它总大小是: 275 mb, 它的默认分片设置number_of_shards=5, 副本数设置number_of_replicas=2,它每个分片大小目前为：275 / (5 * (2 + 1) ) = 27 mb 
注：每个分片大小最优值为<=30G(3072mb), 因此理论上这个索引还能继续增长大小,直到单个分片30G大小。
5. 当前集群维度磁盘使用率54.00%
6. 当前节点维度磁盘使用率正常
更多详细优化文章请参考：https://cloud.tencent.com/developer/article/1507657
------------------------------------------------------------------------
当前集群节点状态：
ip             heap.percent ram.percent cpu load_1m load_5m load_15m node.role master name
10.53.200.58             29          97   3    0.09    0.08     0.11 di        -      es_data06
10.113.12.20             52          99   6    0.02    0.07     0.12 mdi       *      es_master
100.121.178.36           30          99   5    0.29    0.22     0.16 di        -      es_data04
100.121.176.46           24          96   5    0.02    0.12     0.14 di        -      es_data03
10.251.192.19            53          97   3    0.02    0.04     0.06 di        -      es_data01
100.125.68.193           55          92   6    0.26    0.31     0.38 di        -      es_data05
9.71.155.13               5          97   2    0.07    0.10     0.10 i         -      es_kibana_logstash
100.121.174.34           52          92   2    0.10    0.08     0.08 di        -      es_data02
注意：带 * 号的表示是master节点, 我们es集群的node节点是cvm, 对客户是不可见的, 客户无需关心cvm侧节点的运维操作。
------------------------------------------------------------------------
当前集群节点磁盘状态：
ip             diskTotal diskUsed diskAvail diskUsedPercent master name
10.53.200.58     196.7gb   12.6gb   184.1gb            6.41 -      es_data06
10.113.12.20     196.7gb   29.9gb   166.7gb           15.24 *      es_master
100.121.178.36   196.7gb   21.3gb   175.3gb           10.86 -      es_data04
100.121.176.46   196.7gb   31.9gb   164.8gb           16.22 -      es_data03
10.251.192.19    196.7gb   12.8gb   183.9gb            6.51 -      es_data01
100.125.68.193   196.7gb   16.1gb   180.5gb            8.21 -      es_data05
9.71.155.13      499.7gb  888.6mb   498.8gb            0.17 -      es_kibana_logstash
100.121.174.34   196.7gb   15.8gb   180.8gb            8.05 -      es_data02
注意：如果以上节点有部分节点磁盘使用率diskUsedPercent跟其他节点有明显的差距, 说明存在“数据热点”情况, 也就是说索引分片的分片是不均匀的, “数据热点”的出现将会导致部分节点压力过大, 建议分片数的设置要为节点数的整数倍。
------------------------------------------------------------------------
每个节点上分配的分片（shard）的数量和每个分片（shard）所使用的硬盘容量:
shards disk.indices disk.used disk.avail disk.total disk.percent host           ip             node
   286        5.8gb    16.1gb    180.5gb    196.7gb            8 100.125.68.193 100.125.68.193 es_data05
   287       20.2gb    31.9gb    164.8gb    196.7gb           16 100.121.176.46 100.121.176.46 es_data03
   287       10.1gb    21.3gb    175.3gb    196.7gb           10 100.121.178.36 100.121.178.36 es_data04
   286        5.5gb    15.8gb    180.8gb    196.7gb            8 100.121.174.34 100.121.174.34 es_data02
   287         19gb    29.9gb    166.7gb    196.7gb           15 10.113.12.20   10.113.12.20   es_master
   286        2.5gb    12.8gb    183.9gb    196.7gb            6 10.251.192.19  10.251.192.19  es_data01
   286        2.3gb    12.6gb    184.1gb    196.7gb            6 10.53.200.58   10.53.200.58   es_data06
------------------------------------------------------------------------
所有别名：
alias                        index                filter routing.index routing.search
.ml-anomalies-.write-ka-test .ml-anomalies-shared -      -             -
.ml-anomalies-.write-kpi     .ml-anomalies-shared -      -             -
.ml-anomalies-ka-test        .ml-anomalies-shared *      -             -
.ml-anomalies-kpi            .ml-anomalies-shared *      -             -
.security                    .security-6          -      -             -
------------------------------------------------------------------------
以上内容为部分输出, 详细内容已保存至/tmp/eslog/***-eslog-es_kibana_logstash-20200116.log ,  同时也非常欢迎您对本脚本提供宝贵的建议，感谢您的支持！

```


