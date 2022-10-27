JSON（[JavaScript](https://baike.baidu.com/item/JavaScript?fromModule=lemma_inlink) Object Notation, JS对象简谱）是一种轻量级的数据交换格式。它基于 [ECMAScript](https://baike.baidu.com/item/ECMAScript?fromModule=lemma_inlink)（European Computer Manufacturers Association, 欧洲计算机协会制定的js规范）的一个子集，采用完全独立于编程语言的文本格式来存储和表示数据。简洁和清晰的层次结构使得 JSON 成为理想的数据交换语言。 易于人阅读和编写，同时也易于机器解析和生成，并有效地提升网络传输效率。

***

JSON由两种结构组成：

1. 键值对的无序集合——对象(或者叫记录、结构、字典、哈希表、有键列表或关联数组等)
2. 值的有序列表——数组

***

对象是一个无序的键值对的集合，使用大括号包裹，键值对用逗号分隔，键和值用英文冒号分隔。例如：

```json
{
	"name": "roydon",
	"password": 123456
}
```

数组是值（value）的有序集合。一个数组用英文中括号包裹。值（value）可以是双引号括起来的字符串（string）、数值(number)、true、false、 null、对象（object）或者数组（array）。这些结构可以嵌套。例如：

```json
[
	123456,
	"roydon",
	{
		"name": "roydon",
		"password": "qwer1234"
	},
	"18岁",
	"河南",
    [
        "大学",
        "计算机",
        "大三"
    ]
]
```