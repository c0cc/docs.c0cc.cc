# uuid 通用唯一识别码库

### uuid1

    uuid1 函数返回的是不可读的uuid，如果要字符串的uuid，请选择调用 hexuuid1

**函数** : `uuid1`


**函数参数**

无

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`uuid` | `string` | `uuid` 内容
`err` | `string` | `uuid` 获取失败报错内容

**调用样例**

```poc
local uuid = require("uuid")
local uuid_value,err = uuid.uuid1()
if err then
    error(err)
end

print(uuid_value)
```

### hexuuid1

    hexuuid1 函数返回的是可读的uuid1，如果要bytes的uuid1，请选择调用 uuid1
    
    为了通用方便，hexuuid 使用频率较高，直接设置别名为 uuid

**函数** : `hexuuid1`

**别名** : `uuid`

**函数参数**

无

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`uuid` | `string` | `uuid` 内容
`err` | `string` | `uuid` 获取失败报错内容

**调用样例**

```poc
local uuid = require("uuid")
local uuid_value,err = uuid.hexuuid1()
if err then
    error(err)
end

print(uuid_value)
```



### uuid2

    uuid2 函数返回的是不可读的uuid2，如果要字符串的uuid2，请选择调用 hexuuid2

**函数** : `uuid2`


**函数参数**

无

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`uuid` | `string` | `uuid` 内容
`err` | `string` | `uuid` 获取失败报错内容

**调用样例**

```poc
local uuid = require("uuid")
local uuid_value,err = uuid.uuid2()
if err then
    error(err)
end

print(uuid_value)
```

### hexuuid2

    hexuuid2 函数返回的是可读的uuid2，如果要bytes的uuid2，请选择调用 uuid2

**函数** : `hexuuid2`

**函数参数**

无

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`uuid` | `string` | `uuid` 内容
`err` | `string` | `uuid` 获取失败报错内容

**调用样例**

```poc
local uuid = require("uuid")
local uuid_value,err = uuid.hexuuid2()
if err then
    error(err)
end

print(uuid_value)
```


### uuid4

    uuid4 函数返回的是不可读的uuid4，如果要字符串的uuid4，请选择调用 hexuuid4

**函数** : `uuid4`


**函数参数**

无

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`uuid` | `string` | `uuid` 内容
`err` | `string` | `uuid` 获取失败报错内容

**调用样例**

```poc
local uuid = require("uuid")
local uuid_value,err = uuid.uuid4()
if err then
    error(err)
end

print(uuid_value)
```

### hexuuid4

    hexuuid2 函数返回的是可读的uuid4，如果要bytes的uuid4，请选择调用 uuid4

**函数** : `hexuuid4`

**函数参数**

无

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`uuid` | `string` | `uuid` 内容
`err` | `string` | `uuid` 获取失败报错内容

**调用样例**

```poc
local uuid = require("uuid")
local uuid_value,err = uuid.hexuuid4()
if err then
    error(err)
end

print(uuid_value)
```