# zlib 压缩/解压 支持库

### 计算Adler-32 校验和

    用于计算数据流的 Adler-32 校验和(类似CRC32)

**函数** : `adler32`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`data` | `string` | 需要计算的值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `number` | 计算完成的 `adler32`
`err` | `string` | 报错返回信息，如果该值不为空，则前面都为空


**调用样例**

```poc
local zlib = require("zlib")

local value, err = zlib.adler32("hello")

if err ~= nil then
    error(err)
end
print(value)
```

### 对比Adler-32 校验和

    对比 adler32 用于计算数据流的 Adler-32 校验和(类似CRC32)

**函数** : `checkadler32`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`verify` | `number` | 用于验证结果的值
`data` | `string` | 需要计算的值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`check` | `bool` | 匹配是否成功
`err` | `string` | 报错返回信息，如果该值不为空，则前面都为空



**调用样例**

```poc
local zlib = require("zlib")

local ok, err = zlib.checkadler32(103547413, "hello")

if err ~= nil then
    error(err)
end
```

### 计算crc32 校验和

    用于计算数据流的 crc32 校验和

**函数** : `crc32`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`data` | `string` | 需要计算的值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `number` | 计算完成的 `crc32`
`err` | `string` | 报错返回信息，如果该值不为空，则前面都为空


**调用样例**

```poc
local zlib = require("zlib")

local value, err = zlib.crc32("hello")

if err ~= nil then
    error(err)
end
print(value)
```

### 对比crc32 校验和

    对比 crc32 用于计算数据流的 crc32 校验和

**函数** : `checkcrc32`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`verify` | `number` | 用于验证结果的值
`data` | `string` | 需要计算的值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`check` | `bool` | 匹配是否成功
`err` | `string` | 报错返回信息，如果该值不为空，则前面都为空



**调用样例**

```poc
local zlib = require("zlib")

local ok, err = zlib.checkcrc32(907060870, "hello")

if err ~= nil then
    error(err)
end
```


### zlib 压缩

    对数据进行zlib压缩

**函数** : `compress`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`data` | `string` | 需要压缩的数据
`level` | `number` | 压缩等级(1-9) 9压缩率最高，相应的会吃资源


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`data` | `string` | 压缩后的值
`err` | `string` | 报错返回信息，如果该值不为空，则前面都为空



**调用样例**

```poc
local zlib = require("zlib")

local data, err = zlib.compress("hello", 1)

if err ~= nil then
    error(err)
end
```


### zlib 解压缩

    对数据进行zlib解压缩

**函数** : `decompress`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`compressdata` | `string` | 压缩后的数据


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`data` | `string` | 解压缩后的值
`err` | `string` | 报错返回信息，如果该值不为空，则前面都为空



**调用样例**

```poc
local zlib = require("zlib")

local data, err = zlib.decompress("compressdata")

if err ~= nil then
    error(err)
end
```


### flate 压缩

    对数据进行flate压缩

**函数** : `flate`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`data` | `string` | 需要压缩的数据
`level` | `number` | 压缩等级(1-9) 9压缩率最高，相应的会吃资源


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`data` | `string` | 压缩后的值
`err` | `string` | 报错返回信息，如果该值不为空，则前面都为空



**调用样例**

```poc
local zlib = require("zlib")

local data, err = zlib.flate("hello", 1)

if err ~= nil then
    error(err)
end
```

### flate 解压缩

    对数据进行zlib解压缩

**函数** : `deflate`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`compressdata` | `string` | 压缩后的数据


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`data` | `string` | 解压缩后的值
`err` | `string` | 报错返回信息，如果该值不为空，则前面都为空



**调用样例**

```poc
local zlib = require("zlib")

local data, err = zlib.deflate("compressdata")

if err ~= nil then
    error(err)
end
```
