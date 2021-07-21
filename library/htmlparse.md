# htmlparse  HTML解析库


### 创建解析对象

    通过解析对象进行处理操作

**函数** : `new`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`html` | `string` | HTML页面内容


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`parse` | `userdata` | 返回html解析对象,该对象的方法在上方有展示
`err` | `string` | 报错返回信息，如果该值不为空，则result内容为空

**调用样例**

```poc
local htmlparse = require("htmlparse")
local obj, err = htmlparse.new("<html><head><title>mdzz</title></head><body></body></html>")
if err ~= nil then
    error(err)
end
-- 获取title标签中的内容，需要注意的是，该方法有别于text会获取标签的内容和结构
print(obj:find("title"):str())
```

### 查找所有符合要求的元素

    查找符合筛选器的元素并且返回table

**函数** : `findall`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`table` | `table` | 自身表,值为 htmlparse.new 方法返回的值
`selector` | `string` | HTML页面内容


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `table` | 返回html解析对象的列表,该对象列表中的所有对象同样绑定所有方法,形似返回自身,实际为创建了一个新的对象
`err` | `string` | 报错返回信息，如果该值不为空，则result内容为空

**调用样例**

```poc
local htmlparse = require("htmlparse")
local obj, err = htmlparse.new("<html><head><title>mdzz</title></head><body></body></html>")
if err ~= nil then
    error(err)
end
-- 查找所有title元素，返回便于操作的列表对象，取第1个对象并且输出内容
print(obj:findall("title")[1]:str())
```



### 查找符合要求的元素

    查找符合筛选器的元素并且返回元素

**函数** : `find`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`table` | `table` | 自身表,值为 htmlparse.new 方法返回的值
`selector` | `string` | HTML页面内容


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `table` | 返回html解析对象,该对象同样绑定所有方法,形似返回自身,实际为创建了一个新的对象
`err` | `string` | 报错返回信息，如果该值不为空，则result内容为空

**调用样例**

```poc
local htmlparse = require("htmlparse")
local obj, err = htmlparse.new("<html><head><title>mdzz</title></head><body></body></html>")
if err ~= nil then
    error(err)
end
-- 查找title元素，并且输出内容
print(obj:find("title"):str())
```


### 取标签内的内容

    返回标签内的内容(包括子标签的标签结构)

**函数** : `str`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`table` | `table` | 自身表,值为 htmlparse.new 方法返回的值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `string` | 返回标签的内容
`err` | `string` | 报错返回信息，如果该值不为空，则result内容为空

**调用样例**

```poc
local htmlparse = require("htmlparse")
local obj, err = htmlparse.new("<html><head><title>mdzz</title></head><body></body></html>")
if err ~= nil then
    error(err)
end
-- 查找title元素，并且输出内容（内容包含子标签结构）
print(obj:find("title"):str())
```


### 取标签内的内容

    返回标签内的内容(包括 当前标签的标签结构 以及 子标签 的结构)

**函数** : `cstr`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`table` | `table` | 自身表,值为 htmlparse.new 方法返回的值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `string` | 返回标签的内容
`err` | `string` | 报错返回信息，如果该值不为空，则result内容为空

**调用样例**

```poc
local htmlparse = require("htmlparse")
local obj, err = htmlparse.new("<html><head><title>mdzz</title></head><body></body></html>")
if err ~= nil then
    error(err)
end
-- 输出title标签，并且输出标签，需要注意的是，输出的内容包含当前标签的结构以及子标签的结构
print(obj:find("title"):cstr())
```

### 取标签的属性

    返回标签内的属性，用于对标签内容的批量提取

**函数** : `attr`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`table` | `table` | 自身表,值为 htmlparse.new 方法返回的值
`attr` | `string` | 属性名称


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `string` | 返回标签属性对应的值
`exists` | `bool` | 返回标签是否有该属性存在

**调用样例**

```poc
-- 例: 取html内所有a标签的href属性
local htmlparse = require("htmlparse")
local obj, err = htmlparse.new("<html>...</html>")
if err ~= nil then
    error(err)
end
for index,tag in pairs(obj:findall("a[href]")) then
  local val,exists = tag:attr("href")
  if exists then
    print(val)
  end
end
```

### 取标签的下一个标签

    兄弟标签取下一个标签

**函数** : `next`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`table` | `table` | 自身表,值为 htmlparse.new 方法返回的值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `table` | 上一个标签
`err` | `string` | 报错返回信息，如果该值不为空，则result内容为空

**调用样例**

```poc
-- 例: 取html内所有a标签的href属性
local htmlparse = require("htmlparse")
local obj, err = htmlparse.new("<html>...</html>")
if err ~= nil then
    error(err)
end
-- 输出title标签的 下一个标签中 的内容
print(obj:find("title"):next():str())
```

### 取标签的上一个标签

    兄弟标签取上一个标签

**函数** : `prev`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`table` | `table` | 自身表,值为 htmlparse.new 方法返回的值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `table` | 上一个标签
`err` | `string` | 报错返回信息，如果该值不为空，则result内容为空

**调用样例**

```poc
-- 例: 取html内所有a标签的href属性
local htmlparse = require("htmlparse")
local obj, err = htmlparse.new("<html>...</html>")
if err ~= nil then
    error(err)
end
-- 输出title标签的 上一个标签中 的内容
print(obj:find("title"):prev():str())
```

### 取标签的子标签

    取标签的子标签

**函数** : `children`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`table` | `table` | 自身表,值为 htmlparse.new 方法返回的值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `table` | 上一个标签
`err` | `string` | 报错返回信息，如果该值不为空，则result内容为空

**调用样例**

```poc
-- 例: 取html内所有a标签的href属性
local htmlparse = require("htmlparse")
local obj, err = htmlparse.new("<html><head></head><body></body></html>")
if err ~= nil then
    error(err)
end
-- 取html标签的子标签。获取所有的标签并且取第一个,输出当前标签结构
print(obj:find("html"):children():all()[1]:cstr())
```

### 取标签的父标签

    取标签的父标签

**函数** : `parrent`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`table` | `table` | 自身表,值为 htmlparse.new 方法返回的值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `table` | 上一个标签
`err` | `string` | 报错返回信息，如果该值不为空，则result内容为空

**调用样例**

```poc
-- 例: 取html内所有a标签的href属性
local htmlparse = require("htmlparse")
local obj, err = htmlparse.new("<html><head></head><body></body></html>")
if err ~= nil then
    error(err)
end
-- 取head标签的父标签。输出标签结构
print(obj:find("head"):parrent():cstr())
```


### 取标签的切片

    取标签的切片

**函数** : `slice`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`table` | `table` | 自身表,值为 htmlparse.new 方法返回的值
`start` | `number` | 开始的标签位置
`end` | `number` | 结束的标签位置



**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `table` | 选择出来的一部分标签进行返回，还是同样的obj
`err` | `string` | 报错返回信息，如果该值不为空，则result内容为空

**调用样例**

```poc
-- 例: 取html内所有a标签的href属性
local htmlparse = require("htmlparse")
local obj, err = htmlparse.new("<html><head></head><body></body></html>")
if err ~= nil then
    error(err)
end
-- 取html标签的子标签，并且切片
print(obj:find("html"):children():slice(1,2))
```

### 判断标签是否有某class

    判断标签是否class某类

**函数** : `hasclass`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`table` | `table` | 自身表,值为 htmlparse.new 方法返回的值
`classname` | `string` | 用于判断的类



**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`status` | `bool` | 判断标签是否包含某个class
`err` | `string` | 报错返回信息，如果该值不为空，则status内容为空

**调用样例**

```poc
-- 例: 取html内所有a标签的href属性
local htmlparse = require("htmlparse")
local obj, err = htmlparse.new("<html><head class='A'></head><body></body></html>")
if err ~= nil then
    error(err)
end
-- 取html标签的子标签，并且切片
print(obj:find("head"):hasclass("A"))
```

### 从标签选择集合转换

    将标签集合转换为便于访问的表

**函数** : `all`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`table` | `table` | 自身表,值为 htmlparse.new 方法返回的值



**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `table` | 标签集合转换为表返回
`err` | `string` | 报错返回信息，如果该值不为空，则status内容为空

**调用样例**

```poc
-- 例: 取html内所有a标签的href属性
local htmlparse = require("htmlparse")
local obj, err = htmlparse.new("<html><head class='A'></head><body></body></html>")
if err ~= nil then
    error(err)
end
-- 取html标签的子标签，并且切片
print(obj:find("html"):children():all()[1]:cstr())
```

### 取标签的内容

    标签的内容为文本，<a>xxxxx</a>,标签中央的内容

**函数** : `text`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`table` | `table` | 自身表,值为 htmlparse.new 方法返回的值



**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `table` | 标签集合转换为表返回
`err` | `string` | 报错返回信息，如果该值不为空，则status内容为空

**调用样例**

```poc
-- 例: 取html内所有a标签的href属性
local htmlparse = require("htmlparse")
local obj, err = htmlparse.new("<html><head>xxxxxx</head><body></body></html>")
if err ~= nil then
    error(err)
end
-- 取html标签的子标签，并且切片
print(obj:find("head"):text())
```