# regexp 正则表达式支持库

### 编译正则表达式对象

    通过编译后的正则对象匹配速度会快一点

**函数** : `compile`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`expr` | `string` | 表达式 编译正则表达式对象(Golang实现)

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`regexp` | `userdata` | 返回编译后的正则对象,包括方法 `regexp:match` , `regexp:find_all_string_submatch`
`err` | `string` | 报错返回信息，如果该值不为空，则regexp内容为空

**调用样例**

```poc
local regexp = require("regexp")
local reg, err = regexp.compile("(gopher){2}")
if err then
    error(err)
end
if reg:match("gopher") then
    error("must not be matched")
end
if not reg:match("gophergopher") then
    error("must be matched")
end
print("done: regexp:match()")
```



### 匹配表达式

    直接匹配字符串是否符合表达式

**函数** : `match`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`userdata` | `userdata` | 对象自身（可选）
`expr` | `string` | 表达式
`value` | `string` | 被匹配的值

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`match` | `bool` | 表达式匹配是否成功
`err` | `string` | 报错返回信息，如果该值不为空，则 match 内容为空

**调用样例**

```poc
local regexp = require("regexp")
local found, err = regexp.match("(gopher){2}", "gophergopher")
if err then
    error(err)
end
if not found then
    error("must be matched")
end
print("done: regexp.match()")
```


### 正则提取内容

    对匹配值内的数据进行提取

**函数** : `find_all_string_submatch`

**别名** : `findall`

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`userdata` | `userdata` | 对象自身（可选）
`expr` | `string` | 表达式
`matchv` | `string` | 被匹配的值

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `table` | 表达式匹配是否成功
`err` | `string` | 报错返回信息，如果该值不为空，则result内容为空

**调用样例**

```poc
local regexp = require("regexp")
local result, err = regexp.find_all_string_submatch("string: '(.*)\\s+(.*)'$", "my string: 'hello world'")
if err then
    error(err)
end
if not(result[1][2] == "hello") then
    error("not found: "..tostring(result[1][2]))
end
if not(result[1][3] == "world") then
    error("not found: "..tostring(result[1][3]))
end
print("done: regexp.find_all_string_submatch()")
```


