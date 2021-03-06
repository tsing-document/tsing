# 简介

- 概要：
    - 起源：
        - Shay Banon刚结婚不久，为了妻子抽象Lucene代码为了java程序员可以在应用中添加搜索功能，找到工作后，公司需要做一套搜索引擎，然后他把自己写的一套东西做成了一套服务就叫做 Elasticsearch。
        - 1998年9月4日，谷歌公司在美国硅谷成立，他是一家做搜索引擎起价的公司。
        - 美国的一名Doug Cutting美国工程师，也迷上了搜索引擎，他做了一个文本搜索的函数库，命名为Lucene。
        - Lucene是java编写的，目标是为了各种小型应用软件加入全文检索的功能，因为好用而且开源，非常受程序员欢迎。
        - 2004年Doug Cutting又在Lucene基础上和apache合作开发了一款可以代替当时主流搜索的开源引擎命名为 Nutch。
        - 由于大数据时代的到来，Nutch不能够支持大数据的搜索。
        - 2004年Doug Cutting基于谷歌的一篇论文实现了分布式文件存储系统，并且命名为 NDFS。
        - 2005年Doug Cutting又基于谷歌发表的一篇MapReduce变成模型，在Nutch搜索引擎上实现了该功能。
        - 2006年招安了Doug Cutting改造升级，命名为Hadoop。
        - 2006年Doug Cutting又引进了BigTable到Hadoop，然后命名Hbase。
    - 定义：
        - Elaticsearch 简称为 es, es是一个开源的高扩展的分布式全文检索引擎，他几乎是实时的存储、检索数据；本身扩展性很好，可以扩展到上百台服务器，处理PB的数据，es使用java开发并使用Lucene作为其核心来实现所有索引和搜索的功能，但是他的目的就是通过简单的restful api来隐藏Lucene的复杂性，从而让全文检索变得简单。
        - 它用于全文搜索、结构化搜索、分析。
    - 搜索引擎的差别：
        - Elasticsearch：
            -  是一个实时分布式搜索和分析引擎，它可以处理大数据。一般用于全文检索、结构话搜索、分析这三者混合使用。Elasticsearch是一个基于Apache Lucene的开源的搜索引擎，Lucene只是一个库，如果想要使用它，必须使用java来作为开发语言并将其直接集成到你的应用中，比较糟糕的是Lucene非常复杂，你需要深入了解检索相关的知识来理解它是如何工作的。Elasticsearch也是使用java开发并使用Lucene作为其核心来实现所有的索引金额搜索的功能，但是它的目的是通过简单的 Restful api 来隐藏Lucene的复杂性，让全文检索变得简单。
        - Solr：
            - 它是Apache下的顶级开源的项目，采用java开发，其底层也是基于Lucene做的全文搜索服务器，Solr提供了比Lucene更为丰富的查询语言，同时实现了可配置、可扩展、并对索引、搜索性能的优化。Solr是基于Lucene开发企业级搜索服务其，实际上就是封装了Lucene。
        - Lucene：
            - 它是一个开放源代码的全文检索引擎工具包，但是它不是一个完整的全文检索引擎，而是一个全文检索引擎架构，提供了完整的查询引擎和索引引擎，部分文本分析引擎。
    - 核心概念：
        - 类比mysql学习es：
            - es 是面向文档的数据库。
            - mysql(database)数据库 -> es(indices)索引
            - mysql(tables)表 -> es(types)
            - mysql(rows)行 -> es(document)文档
            - mysql(columes)字段 -> es(fields)字段
        - 物理设计：
            - es 在后台把每个索引分成多个分片，每个分片可以在集群中的不同服务器上迁移。
        - 逻辑设计：
            - 文档
            - 类型
            - 索引
- 语法：
- 案例：
