# Json支持库

### json 字符串转表

**函数** : `decode`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`jsonString` | `string` | json字符串


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `table` | 字符串转表之后的表
`err` | `string` | 报错返回信息，如果该值不为空，则result内容为空

**调用样例**

```poc


local json = require("json")

-- 多行字符串高亮有问题 [[到]]中间的是多行字符串
local jsonString = [[
    {
        "a": {"b":1}
    }
]]
local result, err = json.decode(jsonString)
if err then
    error(err)
end
```




### json 表转字符串

**函数** : `encode`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`table` | `table` | 需要encode的表


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `string` | 表转字符串后字符串的内容
`err` | `string` | 报错返回信息，如果该值不为空，则result内容为空

**调用样例**

```poc
local json = require("json")

local table = {a={b=1}}
local result, err = json.encode(table)
if err then
    error(err)
end
```

