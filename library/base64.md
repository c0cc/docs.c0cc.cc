# Base64 编码/解码库


### Base64解码

**函数** : `b64decode`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`encode` | `string` | b64编码后的数据


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`data` | `string` | b64解码后的数据
`err` | `string` | 报错返回信息，如果该值不为空，则`data`内容为空

**调用样例**

```poc
local base64 = require("base64")
local decode, err = base64.b64decode("aGVsbG8=")
if err then
    error(err)
end

print(decode)
```


### Base64编码

**函数** : `b64encode`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`data` | `string` | 需要进行b64编码的数据


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`encode` | `string` | b64编码后的数据

**调用样例**

```poc
local base64 = require("base64")
local encode = base64.b64encode("hello")

print(encode)
```



### Base32解码

**函数** : `b32decode`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`encode` | `string` | b32编码后的数据


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`data` | `string` | b32解码后的数据
`err` | `string` | 报错返回信息，如果该值不为空，则`data`内容为空

**调用样例**

```poc
local base64 = require("base64")
local decode, err = base64.b32decode("NBSWY3DP")
if err then
    error(err)
end

print(decode)
```



### Base32编码

**函数** : `b32encode`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`data` | `string` | 需要进行b32编码的数据


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`encode` | `string` | b32编码后的数据

**调用样例**

```poc
local base64 = require("base64")
local encode = base64.b32encode("hello")

print(encode)
```

