# time 时间库

### 时间戳(秒)

    unix 秒级别时间戳

**函数** : `unix`


**函数参数**

无


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`timestamp` | `number` | 输出当前时间戳 单位(秒)



**调用样例**

```poc
local time = require("time")

local timestamp = time.unix()

```


### 时间戳(毫秒)

    unix 毫秒级别时间戳

**函数** : `unix_nano`


**函数参数**

无


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`timestamp` | `number` | 输出当前时间戳 单位(毫秒)



**调用样例**

```poc
local time = require("time")

local timestamp = time.unix_nano()
```


### 睡眠(延时)

**函数** : `sleep`

    sleep 延时

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`second` | `number` | 延时时间 单位(秒)

**函数返回**

无

**调用样例**

```poc
local time = require("time")

time.sleep(1.1)
```


### 解析时间字符串

**函数** : `parse`

    解析时间字符串，时间字符串转时间戳

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`timestring` | `string` | 需要解析的时间字符串
`timeformat` | `string` | 格式化字符串(参考Golang) 例如 `2006-01-02 15:04:05` -> `年-月-日 时:分:秒`


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`timestamp` | `number` | 格式化后返回时间戳

**调用样例**

```poc
local time = require("time")

local result, err = time.parse("Dec  2 03:33:05 2018", "Jan  2 15:04:05 2006")
if err then
    error(err)
end

if not(result == 1543721585) then
    error("time.parse()")
end
```


### 时间戳转时间字符串

**函数** : `format`

    将时间戳转换为人可读定的时间格式

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`timestamp` | `number` | 时间戳
`timeformat` | `string` | 格式化字符串(参考Golang) 可空 例如 `2006-01-02 15:04:05` -> `年-月-日 时:分:秒`
`formatlocal` | `string` | 时区信息 可空  例如 "Europe/Moscow"


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`timestring` | `string` | 输出格式化后的时间
`error` | `string` | 转换错误信息，如果该值不为`nil`,则`timestring`为空


**调用样例**

```poc
local time = require("time")

local result, err = time.format(1543721585, "Jan  2 15:04:05 2006", "")
if err then
    error(err)
end
if not(result == "Dec  2 06:33:05 2018") then
    error("time.format()")
end
```

