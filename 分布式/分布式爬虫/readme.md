
爬取网站列表页

解析链接内容，模式匹配

按url生成爬取任务

kafka

爬取落地、详情页面

上游的主要工作是根据预先配置好的起点来爬取所有的目标“列表页”，
列表页的html内容中会包含有所有详情页的链接。
详情页的数量一般是列表页的10到100倍，所以我们将这些详情页链接作为“任务”内容，通过消息队列分发出去。
针对页面爬取来说，在执行时是否偶尔会有重复其实不太重要，
因为任务结果是幂等的（这里我们只爬页面内容，不考虑评论部分）。

本节我们来简单实现一个基于消息队列的爬虫，本节我们使用nats来做任务分发。
实际开发中，应该针对自己的业务对消息本身的可靠性要求和公司的基础架构组件情况进行选型。