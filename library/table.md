# table 表操作库


### 获取table长度

**函数** : `getn`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`table` | `table` | 等待获取长度的表


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`len` | `number` | 获取到的table长度

**调用样例**

```poc
local tab = {}
tab[1] = "hello"
tab[2] = "world"

print(table.getn(tab))
```

### 使用字符串拼接表

    该方法将 sep 拼接到 table中值之间，拼接成一个完整的字符串

**函数** : `concat`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`table` | `table` | 表
`sep` | `string` | 拼接的间隔字符串
`start` | `number` | 可选,拼接开始的位置
`end` | `number` | 可选,拼接结束的位置


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `string` | 拼接完成的字符串

**调用样例**

```poc
local tab = {}
tab[1] = "hello"
tab[2] = "world"

print(table.concat(tab,","))

-- 输出 hello,world
```

### 表中插入元素

    将元素插入到指定位置，或添加到 table 最后

**函数** : `insert`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`table` | `table` | 表
`index` | `number` | 可选,插入`table` 的位置
`value` | `all` | 插入的值，如果`index`为空，则value添加到`table`最后的位置


**函数返回**

无

**调用样例**

```poc
local tab = {}
tab[1] = "hello"
tab[2] = "world"

table.insert(tab, "aaa")

print(table.concat(tab,","))

-- 输出 hello,world,aaa
```

### 获取表中最大的正整数key

    指定table中所有正数key值中最大的key值. 如果不存在key值为正数的元素, 则返回0

**函数** : `maxn`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`table` | `table` | 表


**函数返回**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`maxn` | `number` | `key` 的值

**调用样例**

```poc
local tab = {}
tab[1] = "hello"
tab[2] = "world"

table.insert(tab, "aaa")

print(table.maxn(tab))

-- 输出 3
```


### 从表中移除元素

    从表中按整数key移除元素

**函数** : `remove`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`table` | `table` | 表
`index` | `number` | 移除的索引，默认移除最后一个元素


**函数返回**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`table` | `table` | 返回表自身

**调用样例**

```poc
local tab = {}
tab[1] = "hello"
tab[2] = "world"

table.remove(tab)


```

### 表排序

**函数** : `sort`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`table` | `table` | 表
`func` | `function` | 排序函数 function (v1,v2) end


**函数返回**

无

**调用样例**

```poc
fruits = {"banana","orange","apple","grapes"}
print("排序前")
for k,v in ipairs(fruits) do
        print(k,v)
end

table.sort(fruits)
print("排序后")
for k,v in ipairs(fruits) do
        print(k,v)
end

```