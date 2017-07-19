# 目录

- [介绍](#介绍)
- [elasticSearch-header](#elasticSearch-header)
- [multi_match](#multi_match)
- [基础入门](#基础入门)


## 介绍
- ElasticSearch是一个基于Lucene的搜索服务器。它提供了一个分布式多用户能力的全文搜索引擎，基于RESTful web接口。Elasticsearch是用Java开发的，并作为Apache许可条款下的开放源码发布，是当前流行的企业级搜索引擎。设计用于云计算中，能够达到实时搜索，稳定，可靠，快速，安装使用方便.

- Lucene的目的是为软件开发人员提供一个简单易用的工具包    ,信息检索程序库

- RESTful web: 
  REST是一种架构风格，其核心是面向资源，REST专门针对网络应用设计和开发方式，以降低开发的复杂性，提高系统的可伸缩性。REST提出设计概念和准则为：
  1.网络上的所有事物都可以被抽象为资源(resource)
  2.每一个资源都有唯一的资源标识(resource identifier)，对资源的操作不会改变这些标识
  3.所有的操作都是无状态的


## elasticSearch-header

```
操作(起服):

  git clone git://github.com/mobz/elasticsearch-head.git
  cd elasticsearch-head
  npm install
  npm run start
  open http://localhost:9100/
```



## multi_match

```
{
  "dis_max": {
    "queries":  [
      {
        "match": {
          "title": {
            "query": "Quick brown fox",
            "minimum_should_match": "30%"
          }
        }
      },
      {
        "match": {
          "body": {
            "query": "Quick brown fox",
            "minimum_should_match": "30%"
          }
        }
      },
    ],
    "tie_breaker": 0.3
  }
}

使用 multi_match：
{
    "multi_match": {
        "query":                "Quick brown fox",
        "type":                 "best_fields", 
        "fields":               [ "title", "body" ],
        "tie_breaker":          0.3,
        "minimum_should_match": "30%" 
    }
}
```


## 基础入门

- 健康状态   
ES 健康状态status 分为三个状态 green,yellow或者red  
 - green:所有的主分片和副本分片都正常运行  
 - yellow:所有的主分片都正常运行，但不是所有的副分片都正常运行  
 - red:有主分片没能正常运行

```
  GET /_cluster/health
```

```
{
  "cluster_name":             "elasticsearch",
  "status":                   "green",
  "timed_out":             false,
   "number_of_nodes":       1,
   "number_of_data_nodes":  1,
   "active_primary_shards": 0,
   "active_shards":         0,
   "relocating_shards":     0,
   "initializing_shards":   0,
   "unassigned_shards":     0
}
```

## 索引
- elastic mapping - field datatypes

`text` `keyword` `date` `long` `double` `boolean` `ip`

```
  PUT /YOUR_INDEX_NAME

  {
    "mappings":{
      "YOUR_TYPE_NAME":{
        "properties":{
          "YOUR_FIELD_NAME":{
            "type":"YOUR_FIELD_TYPE"
          }
        }
      }
    }
  }
```

### ES自动关系映射错误

- [需要再ES先创建索引及映射关系,然后导入数据](#https://discuss.elastic.co/t/number-format-exception-for-string-type/59175/6)  
- [新建一个索引，然后将旧的索引指向新的索引](#https://www.elastic.co/guide/en/elasticsearch/reference/5.x/mapping.html#_updating_existing_mappings)  

## 文档

```
Relational DB ->Databases(数据库)  ->Tables(表)   ->Rows(记录)    ->Columns(字段)
Elasticsearch ->Indices(索引)   ->Types(类型)    ->Documents(文档) ->Fields(字段)
```

#### 在ES中没有一条数据称之为一条文档

- 文档元数据

>> 一个文档不仅仅包含它的数据，也包含元数据 ---有关文档的信息，其中必须有三个元素:

 - _index : 索引，所有数据库  
 - _type:类型，所属表  
 - id:唯一id，表中唯一标示  

### GET 查询文档

```
GET /index_name/type_name/id
```

返回数据在_source字段中，如：  

```
GET /website/blog/123?pretty
```

```
{
 "index": "website",
  "_type":"blog",
  "_id":"123",
  "_version":1,
  "found":true,
  "_source":{
    "title":"My first blog entry",
    "text":"Just trying this out...",
    "date":"2014/01/01"
  } 
}
  
```

####可选参数

- pretty:格式化JSON  
- _source:指定返回字段  

如：指定返回title text字段 date将被过滤  

```
GET /website/blog/123?_source=title,text
```

```
  {
    "_index":"website",
    "_type":"blog",
    "_id":"123",
    "_version":1,
    "found":true,
    "_source":{
      "title":"Myfirst blog entry",
      "text":"Just trying this out..."      
    }
  }
```

- found字段表示 是否找到匹配数据,(bool)

#### 可选端点
_如果你只想得到_source字段,不需要任何元数据，你可以使用_source端点_,如:

```
GET /website/blog/123/_source
```

```
  {
      "title": "My first blog entry",
      "text":  "Just trying this out...",
      "date":  "2014/01/01"
  }
```

## 更新文档
- 文档不能被修改，只能被替换 简单理解的话就是对象的覆盖合并，新的参数覆盖老的参数  

```
PUT /index_name/type_name/id
{
  ...some data...
}
```

如：

```
 PUT /website/blog/123
 {
  "title": "My first blog entry",
    "text":  "I am starting to get the hang of this...",
    "date":  "2014/01/02"
  }
```

```
  {
    "_index" :   "website",
    "_type" :    "blog",
    "_id" :      "123",
    "_version" : 2,
    "created":   false 
  }
```


- _version:每次数据变更版本号，ES自动维护  
- created: 相同唯一标示的数据是否存在，(bool值，false表示已经存在，则是更新，否则创建)  

####部分更新
由于文档只能替换，因此使用POST"重新创建(替换)",替换的参数需要通过`doc`属性传递

```
  POST /index_name/type/id/_update
```

例如，我们怎家字段tags和views到博客

```
 POST /website/blog/1_update
 {
    "doc":{
      "tags":["testing"],
      "views":0
    }
 }
```

## 创建文档

创建文档有三种方式:

- 自动生成ID

```
POST /index_name/type_name
{...}
```

如：

```
POST /website/blog
```

- 指定id  
- 指定操作选项op_type   

```
  POST /index_name/type_name/id?op_type=create
  {...}
```

- 指定端点 `_create`

```
 POST /index_name/type_name/id/create
 {...}
```
