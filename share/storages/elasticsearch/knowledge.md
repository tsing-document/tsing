# 基础知识

- 概要：
    - Rest风格说明：
        |  method   | url地址  | 描述 
        |  ----     |  ----   |  ----  | 
        | PUT  | localhost:9200/索引名称/类型名称/文档id | 创建文档（指定文档id）
        | POST  | localhost:9200/索引名称/类型名称 |    创建文档（随机文档id）
        | POST  | localhost:9200/索引名称/类型名称/文档id/_update |    修改文档
        | DELETE  | localhost:9200/索引名称/类型名称/文档id |    删除文档
        | GET  | localhost:9200/索引名称/类型名称/文档id |    查询文档根据文档id
        | POST  | localhost:9200/索引名称/类型名称/_search |    查询所有数据
    - 创建索引规则：
    - Kibana简单的CRUD：
        ```java
            //status
                desc：
                url：
                    http://ip:port
                body：
                    {
                        "name": "iz8vb9qm4nc2ak59ljq2jsz",
                        "cluster_name": "elasticsearch",
                        "cluster_uuid": "iTHuoOCESNuHBKYrO-SLUw",
                        "version": {
                            "number": "7.9.3",
                            "build_flavor": "default",
                            "build_type": "tar",
                            "build_hash": "c4138e51121ef06a6404866cddc601906fe5c868",
                            "build_date": "2020-10-16T10:36:16.141335Z",
                            "build_snapshot": false,
                            "lucene_version": "8.6.2",
                            "minimum_wire_compatibility_version": "6.8.0",
                            "minimum_index_compatibility_version": "6.0.0-beta1"
                        },
                        "tagline": "You Know, for Search"
                    }
            //add-put
                desc：
                    可以新增可以修改，PUT必须指定id;由于PUT需要指定id,所以一般都是用来做修改；这个会对文档所有的数据进行更改。
                url：
                    http://ip:port/demo_tsing/_doc/5
                body：
                    {
                        "name":"tsing12",
                        "sex":"男"
                    }
            //add-post
                desc：
                    新增，如果不指定id，会自动生成id。指定id就会修改这个数据，并新增版本号。
                url：
                    http://ip:port/demo_tsing/_doc/2
                body：
                    {
                        "name":"tsing11111",
                        "sex":"男",
                        "age": 11111
                    }
            //delete
                desc：
                url：
                    http://39.98.165.77:9200/demo_tsing/_doc/2
                body：
                    {
                        "_index": "demo_tsing",
                        "_type": "_doc",
                        "_id": "2",
                        "_version": 3,
                        "result": "deleted",
                        "_shards": {
                            "total": 2,
                            "successful": 1,
                            "failed": 0
                        },
                        "_seq_no": 3,
                        "_primary_term": 1
                    }
            //update-post
                desc：
                    更新部分字段。
                url：
                    http://39.98.165.77:9200/demo_tsing/_doc/5/_update
                body：
                    {
                        "doc":{
                            "name":"更新数据",
                            "age":2333
                        }
                    }
            //search-get
                desc：
                    用get方式查询数据。
                url：
                    http://39.98.165.77:9200/demo_tsing/_search?q=*&sort=age:desc&pretty
                body：
                    {
                        "took": 15,
                        "timed_out": false,
                        "_shards": {
                            "total": 5,
                            "successful": 5,
                            "skipped": 0,
                            "failed": 0
                        },
                        "hits": {
                            "total": {
                            "value": 5,
                            "relation": "eq"
                            },
                            "max_score": null,
                            "hits": [
                            {
                                "_index": "demo_tsing",
                                "_type": "_doc",
                                "_id": "5",
                                "_score": null,
                                "_source": {
                                "name": "更新数据",
                                "sex": "不安不女",
                                "age": 2333
                                },
                                "sort": [
                                2333
                                ]
                            },
                            {
                                "_index": "demo_tsing",
                                "_type": "_doc",
                                "_id": "4",
                                "_score": null,
                                "_source": {
                                "name": "tsing1",
                                "age": 251,
                                "sex": "男"
                                },
                                "sort": [
                                251
                                ]
                            },
                            {
                                "_index": "demo_tsing",
                                "_type": "_doc",
                                "_id": "6IVuonUBKFJNFzY_pADq",
                                "_score": null,
                                "_source": {
                                "name": "tsing12",
                                "sex": "男"
                                },
                                "sort": [
                                -9223372036854775808
                                ]
                            },
                            {
                                "_index": "demo_tsing",
                                "_type": "_doc",
                                "_id": "6YVuonUBKFJNFzY_rABX",
                                "_score": null,
                                "_source": {
                                "name": "tsing12",
                                "sex": "男"
                                },
                                "sort": [
                                -9223372036854775808
                                ]
                            },
                            {
                                "_index": "demo_tsing",
                                "_type": "_doc",
                                "_id": "6oVuonUBKFJNFzY_sQAb",
                                "_score": null,
                                "_source": {
                                "name": "tsing12",
                                "sex": "男"
                                },
                                "sort": [
                                -9223372036854775808
                                ]
                            }
                            ]
                        }
                        }
            //search-get
                desc：
                    参数放在请求体中。
                url：
                    http://39.98.165.77:9200/demo_tsing/_search
                body：
                    {
                        "took": 7,
                        "timed_out": false,
                        "_shards": {
                            "total": 5,
                            "successful": 5,
                            "skipped": 0,
                            "failed": 0
                        },
                        "hits": {
                            "total": {
                                "value": 5,
                                "relation": "eq"
                            },
                            "max_score": null,
                            "hits": [
                                {
                                    "_index": "demo_tsing",
                                    "_type": "_doc",
                                    "_id": "5",
                                    "_score": null,
                                    "_source": {
                                        "name": "更新数据",
                                        "sex": "不安不女",
                                        "age": 2333
                                    },
                                    "sort": [
                                        2333
                                    ]
                                },
                                {
                                    "_index": "demo_tsing",
                                    "_type": "_doc",
                                    "_id": "4",
                                    "_score": null,
                                    "_source": {
                                        "name": "tsing1",
                                        "age": 251,
                                        "sex": "男"
                                    },
                                    "sort": [
                                        251
                                    ]
                                },
                                {
                                    "_index": "demo_tsing",
                                    "_type": "_doc",
                                    "_id": "6IVuonUBKFJNFzY_pADq",
                                    "_score": null,
                                    "_source": {
                                        "name": "tsing12",
                                        "sex": "男"
                                    },
                                    "sort": [
                                        -9223372036854775808
                                    ]
                                },
                                {
                                    "_index": "demo_tsing",
                                    "_type": "_doc",
                                    "_id": "6YVuonUBKFJNFzY_rABX",
                                    "_score": null,
                                    "_source": {
                                        "name": "tsing12",
                                        "sex": "男"
                                    },
                                    "sort": [
                                        -9223372036854775808
                                    ]
                                },
                                {
                                    "_index": "demo_tsing",
                                    "_type": "_doc",
                                    "_id": "6oVuonUBKFJNFzY_sQAb",
                                    "_score": null,
                                    "_source": {
                                        "name": "tsing12",
                                        "sex": "男"
                                    },
                                    "sort": [
                                        -9223372036854775808
                                    ]
                                }
                            ]
                        }
                    }
            //paging-query
                desc：
                    分页查询。
                url：
                    http://39.98.165.77:9200/demo_tsing/_search
                body：
                    {
                        "query":{ "match_all":{} },
                        "from": 4,
                        "size": 2
                    }
        ```
    - Kibana复杂的查询：
- 语法：
- 案例：
