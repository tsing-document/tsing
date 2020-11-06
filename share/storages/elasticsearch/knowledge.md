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
    - Kibana复杂的查询：
- 语法：
- 案例：
