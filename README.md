# 功能简介
根据用户喜好实时推荐商品，同时还展示当前的热门商品。它有两种推荐方法，一种是使用用户画像查找相似用户，然后推荐相似用户的喜好商品，另一种是根据协同过滤算法计算产品相似度，根据已有的喜好商品推荐相似商品，在系统实现中，采用的是两种联合使用的方法。

# 系统模块划分

系统模块划分为商品展示系统，数据计算系统
商品展示系统分为商品展示模块和商品读取模块
数据计算系统分为日志记录模块、热度榜统计模块、用户行为记录模块、产品相似度计算模块

# 模块简介
商品展示模块采用Vue展现，商品读取模块采用Spring Boot+Mybatis+MySQL+HBase读取商品数据和用户推荐商品并将其传输到前端。
其中热度榜由于是短期不会变，同时需经常访问的数据，所以采用Redis进行缓存，加快用户的访问速度。
两大系统之间采用Kafka进行消息传递，方便了系统设计，数据计算系统中主要采用Flink框架对商品展示系统传来的消息进行分类处理，其中只有产品相似度计算模块采用Java定时器定期更新商品的相似分数。
