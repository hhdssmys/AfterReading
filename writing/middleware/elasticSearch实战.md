#### 初读《ElasticSearch 实战》 
&emsp;&emsp;本书结构清晰，内容丰富，对于了解使用的开发者来说足够，非常值得阅读；但是内容有限，和出版时间，一些具体操作可能过时，涉及操作可能不够广泛，这就需要看官方文档与博客进行知识的补足。  
##### 以下是章节介绍：
+ 第一部分：概述
> 1. 介绍，可以解决什么问题，使用案例  
> 2. 深入功能，简单介绍 逻辑概念 与 物理设计，及相关操作  
- 第二部分：功能详细介绍  
> 3. 索引，更新，删除 （API使用，<B>重要</B>）
> 4. 搜索 （API使用，<B>重要</B>）
> 5. 分析数据：字符过滤，分词，分词过滤器，分词索引形成倒排索引（分析器的组成，<B>重要</B>）
> 6. 相关性介绍：打分（TF-IDF词频，逆文档频率），影响打分，字段数据（<B>重要</B>）
> 7. 聚集统计（API使用）
> 8. 文档间关系（肯定很重要，但是用不到就不重要）  
+ 第三部分：集群操作
> 9. 向外扩展：别名，路由（<B>重要</B>）


```
端点或参数：		      请求:		    作用:
_search			GET|POST		查询
_update			POST			更新
_close			POST			关闭索引
_open			POST			打开索引
_query 			DELETE			删除查询的匹配文档
_mapping					类型
_cluster 	                                集群信息
_cat 	                                        集群信息，但是格式较_cluster好看
_alias	                                        别名				
?routing=xxx,xxx 	                        指定路由值，决定索引分片位置          



_search的搜索属性(5部分)：
query   查询DSL，过滤DSL
from 	从0开始计数，默认0
size	默认10
_source
sort	默认排序基于文档得分_score降序

_search的返回响应结构：
{
	"took":2,        -- 查询所用的毫秒数
	"time_out":false,--是否有分片返回超时，可以说明返回的结果是部分的，可能不正确
	"_shards":{			-- 成功响应该请求和未成功响应的分片数量
		"tatal":2,
		"successful":2,
		"failed":0
	},
	"hits":{ --查询命中的返回结果，文档数组
		"total":7,  --所有的匹配结果数目
		"max_score":0.908, --搜索结果中的最大得分
		"hits":[	--查询命中的文档数组
			{
				"_index":xxx,	--索引
				"_type":xxx,	--类型
				"_id":xx,		-- 文档id
				"_score":xx,	-- 相关性得分
				"_source":{
					"feild1":"value1",
					"feild2":"value2"
				}

			},
			......
		]
	}	
}

_search的搜索形式：
查询字符串	?q=field:xxx&from=xxx&size=xxx&_source=field1,field2&sort=field:asc
查询请求体	-d '{
				"query":{

				},
				"from":10,
				"size":10,
				"_source":["field1","field2"],
				"sort":[
					"field1":"desc",
					"feild2":"asc",
					"_score"
				]
			}'

			--这里可以使用通配符，如："_source":["name.*","add*"]
			"_source":{ 
				"include":["field1","field2"],
				"exclude":["field1","field2"]
			}
			--查询的具体使用
			"query":{
				"match_all":{}, -- 匹配所有文档
				"query_string":{}, -- 查询权利过大，风险高，不推荐使用
				"term":{},  -- term 查询，默认词条不过分析器，
				"filtered":{  -- term 过滤器，必须包含在filtered中，包括查询query与过滤filter，过滤器通过缓存查询结果的过滤匹配位集合，可以加速查询，省略得分计算
					"query":{},
					"filter":{
						"_cache":true|false, --是否缓存过滤器
						"term":{}，
						"exists":{ -- 指定字段存在特定值的匹配
							"feild1":"value1" 
						},
						"missing":{ -- 指定字段缺失特定值的匹配
							"feild1":"value1",
							"existence":true|false,  -- 完全缺失
							"null_value":true|false, -- 字段值为 null_value
						},
					}
				},
				"terms":{ -- 可以匹配多个词条，词条间是 OR 
					"field1":["value1","value2"],
					"minimum_should_match":2 --至少匹配词条的数目
				},
				"match":{
					"field1":"value1", -- 默认使用布尔行为 和 OR 操作符
					"field2":{
						"query":"value",
						"operator":"and" --可以修改行为符号
					},
					"field3":{
						"type":"phrase", -- match_phrase 词组查询
						"query":"value",
						"slop":n  -- query_string中的余地，单词间可以间隔的词数
					},
					"field43":{
						"type":"phrase_prefix", -- phrase_prefix 词组最后词的前缀匹配查询
						"query":"ElasticSearch den",  --词组中最后一个词的前缀匹配，这里是 包含ElasticSearch和一个以den开头的词条
						"max_expansions":n  -- 最大的前缀扩展数量
					},
				},
				"multi_match":{ -- 多字段里匹配查询字符串
					"query":"查询字符串",
					"fields":["field1","field2"], --指定的字段组
					"type":"phrase|phrase_prefix"	--和 match 类似
				},
				"range":{ --range 可以是查询也可以是filtered里的过滤器，但是范围查询是二元的（在，不在范围），所以用过滤器更好，gte对于大于等于，ge，lte小于等于，lt小于
					"feild1":{
						"ge":"下界",
						"le":"上界"
					}
				},
				"prefix":{ -- prefix可以是查询也可以是filtered里的过滤器,但是不过分析器，必须是精确匹配
					"feild1":"value1" 
				},
				"wildcard":{ -- 类似通配符匹配的查询，*任意数目字符，？单个字符
					"feild1":"value1" 
				}

			}

			--组合查询
			"query":{
				"bool":{
					"must":[],		-- must任何子句都必须匹配， queryA and query B 
					"should":[],	-- 至少匹配minimum_should_match数量的条件  queryA or query B 
					"must_not":[],	-- 不能被匹配的值 not queryA and not query B 
					"minimum_should_match":n -- 最小的should子句匹配数
				}
			}
			--组合过滤
			"query":{ --使用和组合查询差不多，但是没有minimum_should_match设置，默认为1
				"filtered":{ 
					"query":{},
					"filter":{
						"bool":{
							"must":[],
							"should":[],
							"must_not":[], 
						}
					}
				},
			}
```
