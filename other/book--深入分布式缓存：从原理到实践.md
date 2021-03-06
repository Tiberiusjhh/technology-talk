## 深入分布式缓存：从原理到实践

---

### 目录

```

前言

第1章　缓存为王1

1.1　什么是缓存？1

1.2　为什么使用缓存？2
1.2.1　从用户体验说起3
1.2.2　关于系统的性能3

1.3　从网站的架构发展看缓存4

1.4　客户端缓存5
1.4.1　页面缓存6
1.4.2　浏览器缓存7
1.4.3　APP上的缓存8

1.5　网络中的缓存11
1.5.1　Web代理缓存11
1.5.2　边缘缓存12

1.6　服务端缓存14
1.6.1　数据库缓存14
1.6.2　平台级缓存16
1.6.3　应用级缓存18

第2章　分布式系统理论24

2.1　分布式系统概论24

2.2　分布式系统概念26
2.2.1　进程与线程26
2.2.2　并发26
2.2.3　锁26
2.2.4　并行27
2.2.5　集群27
2.2.6　状态特性28
2.2.7　系统重发与幂等性28
2.2.8　硬件异常30

2.3　分布式系统理论31
2.3.1　CAP理论32
2.3.2　CAP理论澄清34
2.3.3　Paxos35
2.3.4　2PC38
2.3.5　3PC39
2.3.6　Raft40
2.3.7　Lease机制41
2.3.8　解决“脑裂”问题43
2.3.9　Quorum NWR44
2.3.10　MVCC45
2.3.11　Gossip46

2.4　分布式系统设计策略49
2.4.1　心跳检测50
2.4.2　高可用设计50
2.4.3　容错性52
2.4.4　负载均衡53

2.5　分布式系统设计实践54
2.5.1　全局ID生成54
2.5.2　哈希取模56
2.5.3　一致性哈希57
2.5.4　路由表58
2.5.5　数据拆分58

第3章　动手写缓存60

3.1　缓存定义的规范60
3.1.1　新规范的主要内容及特性60
3.1.2　新规范的API介绍61

3.2　缓存框架的实现62
3.2.1　前期准备63
3.2.2　缓存的架构介绍63
3.2.3　设计思路以及知识点详解64

3.3　缓存框架的使用示例74

第4章 　Ehcache与Guava Cache76

4.1　Ehcache的主要特性76

4.2　Ehcache使用介绍77
4.2.1　Ehcache架构图77
4.2.2　缓存数据过期策略78
4.2.3　Ehcache缓存的基本用法81
4.2.4　在Spring中使用Ehcache83

4.3　Ehcache集群介绍85
4.3.1　集群的方式86
4.3.2　如何配置集群88

4.4　 Ehcache的适用场景89

4.5　Guava Cache的使用92
4.5.1　Guava Cache的适用场景92
4.5.2　Guava Cache的创建方式93
4.5.3　缓存数据删除95
4.5.4　并发场景下的使用95
4.6　本章小结96

第5章　从Memcached开始了解集中式缓存97

5.1　Memcached基本知识98
5.1.1　Memcached的操作命令98
5.1.2　Memcached使用场景100
5.1.3　Memcached特征100
5.1.4　Memcached的一些问题101

5.2　Memcached内存存储102
5.2.1　Slab Allocation机制102
5.2.2　使用 Growth Factor进行调优104
5.2.3　Item105

5.3　典型问题解析106
5.3.1　过期机制106
5.3.2　哈希算法107
5.3.3　热点问题108
5.3.4　缓存与数据库的更新问题108
5.3.5　别把缓存当存储109
5.3.6　命名空间110
5.3.7　CAS110

5.4　Memcached客户端分析110
5.4.1　Memcached的Client111
5.4.2　Spymemcached设计思想解析111

5.5　Memcached周边工具发展117

第6章　Memcached 周边技术119

6.1　Twemcache119
6.1.1　Twemcache 的设计原理120
6.1.2　Twemcache的安装及命令行详解122
6.1.3　基于Java的Twemcache用法125

6.2　Twemproxy126
6.2.1　Twemproxy的常用部署模式127
6.2.2　Twemproxy的可扩展性129
6.2.3　Twemproxy源代码简析131

6.3　Mcrouter137
6.3.1　Mcrouter路由算法138
6.3.2　典型的使用场景139
6.3.3　Mcrouter的可扩展性142
6.3.4　源码简要解析144

第7章　Redis探秘148

7.1　数据结构148
7.1.1　value对象的通用结构149
7.1.2　String149
7.1.3　List152
7.1.4　Map155
7.1.5　Set157
7.1.6　Sorted-Set159

7.2　客户端与服务器的交互160
7.2.1　客户端/服务器协议161
7.2.2　请求/响应模式163
7.2.3　事务模式164
7.2.4　脚本模式168
7.2.5　发布/订阅模式169

7.3　单机处理逻辑171
7.3.1　多路复用171
7.3.2　定时任务处理173

7.4　持久化174
7.4.1　基于全量模式的持久化174
7.4.2　基于增量模式的持久化176
7.4.3　基于增量模式持久化的优化178

第8章　分布式Redis180

8.1　水平拆分（sharding）181
8.1.1　数据分布181
8.1.2　请求路由182

8.2　主备复制（replication）182
8.2.1　主备复制流程183
8.2.2　断点续传183

8.3　故障转移（failover）184
8.3.1　sentinel间的相互感知185
8.3.2　master的故障发现186
8.3.3　failover决策186

8.4　Redis Cluster187
8.4.1　拓扑结构187
8.4.2　配置的一致性188
8.4.3　sharding190
8.4.4　failover193
8.4.5　可用性和性能196

第9章　Tair探秘198
9.1　Tair总体架构198
9.2　Config Server简介199
9.3　Data Server简介201
9.4　Tair高可用和负载均衡204
9.4.1　对照表204
9.4.2　数据迁移219
9.5　存储引擎220
9.6　Tair的API222
9.6.1　key/value相关API223
9.6.2　prefix相关的API226

第10章　EVCache探秘229

10.1　EVCache项目介绍230
10.1.1　EVCache的由来231
10.1.2　EVCache的发展232
10.1.3　EVCache的演进234

10.2　EVCache 的使用场景238
10.2.1　典型用例238
10.2.2　典型部署239

10.3　EVCache的性能240
10.3.1　EVCache集群的性能240
10.3.2　全局化复制时的性能问题242
10.3.3　Moneta项目中的组件性能243

10.4　EVCache 的高可用性244
10.4.1　AWS的多可用区244
10.4.2　EVCache对AWS高可用性的增强245

10.5　源码与示例245
10.5.1　源码浅析245
10.5.2　EVCache 示例253

第11章　Aerospike原理及广告业务应用259

11.1　Aerospike架构259

11.2　Aerospike具体实现261
11.2.1　Aerospike集群管理261
11.2.2　数据分布263

11.3　Aerospike集群配置和部署265
11.3.1　搭建集群的方式与配置266
11.3.2　部署集群267

11.4　Aerospike与Redis的对比271

11.5　Aeropsike在广告行业的具体应用272
11.5.1　Aerospike在个性化推荐广告中的应用273
11.5.2　Aerospike在实时竞价广告中的应用274

第12章　社交场景架构进化：从数据库到缓存283

12.1　社交业务示例283
12.1.1　业务模型283
12.1.2　业务场景284
12.1.3　业务特点285

12.2　关系（relation）的存储286
12.2.1　基于DB的最简方案286
12.2.2　DB的sharding方案288
12.2.3　引入缓存290

12.2.4　缓存的优化方案292

12.3　帖子（post）的存储293
12.3.1　基于DB的方案294
12.3.2　引入服务端缓存296
12.3.3　本地缓存297

12.4　时间线（timeline）的存储297
12.4.1　基于DB的方案—push模式298
12.4.2　基于DB的方案—pull模式300
12.4.3　增量查询引入服务端缓存302

第13章　缓存在社交网络Feed系统中的架构实践304

13.1　Feed系统架构304

13.2　Feed缓存模型307

13.3　Feed缓存架构的设计309
13.3.1　简单数据类型的缓存设计310
13.3.2　集合类数据的缓存设计312
13.3.3　其他类型数据的缓存设计314

13.4　Feed缓存的扩展 315
13.4.1　Redis的扩展315
13.4.2　计数器的扩展316
13.4.3　存在性判断的扩展318

13.5　Feed缓存的服务化319

第14章　典型电商应用与缓存324

14.1　电商类应用的挑战及特点324

14.2　应用数据静态化架构高性能单页Web应用325
14.2.1　整体架构326
14.2.2　CMS系统326
14.2.3　前端展示系统328
14.2.4　控制系统328

14.3　应用多级缓存模式支撑海量读服务329
14.3.1　多级缓存介绍329
14.3.2　如何缓存数据331
14.3.3　分布式缓存与应用负载均衡332
14.3.4　热点数据与更新缓存334
14.3.5　更新缓存与原子性336
14.3.6　缓存崩溃与快速修复336

14.4　构建需求响应式亿级商品详情页337
14.4.1　商品详情页前端结构338
14.4.2　单品页技术架构发展338
14.4.3　详情页架构设计原则343
14.4.4　遇到的一些问题349

第15章　同程凤凰缓存系统基于Redis的设计与实践357

15.1　同程凤凰缓存系统要解决什么问题357
15.1.1　Redis用法的凌乱358
15.1.2　从实际案例再看Redis的使用360
15.1.3　如何改变Redis用不好的误区362
15.1.4　凤凰缓存系统对Redis系统化改造364

15.2　用好Redis先运维好它366
15.2.1　传统的Redis运维方式366
15.2.2　Redis的Docker化部署368
15.2.3　凤凰缓存系统对Redis的监控369
15.2.4　凤凰缓存系统对Redis的集群分片优化370
15.2.5　客户端在运维中的作用371
15.2.6　凤凰缓存系统在Redis运维上的工具372

15.3　凤凰缓存系统的使用效果373

第16章　新的旅程374

16.1　更好的引入缓存技术374
16.1.1　缓存引入前的考量374
16.1.2　缓存组件的选择375
16.1.3　缓存架构的设计376
16.1.4　缓存系统的监控及演进377

16.2　缓存分类总结377

16.3　缓存知识结构更多Tips378
16.3.1　缓存使用模式379
16.3.2　缓存协议379
16.3.3　缓存连接池380
16.3.4　几个关注点383
16.3.5　管理缓存387
16.3.6　缓存可用性390
16.3.7　数据一致性392
16.3.8　热点数据处理393
16.3.9　注意事项Tips396


```