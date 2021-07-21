# crypto 加密支持库


### MD5 哈希

**函数** : `md5`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`data` | `string` | 需要进行hash的内容


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`hash` | `string` | 不可读 hash 值

**调用样例**

```poc
local crypto = require("crypto")

print(crypto.md5("1\n"))
```

### HEXMD5 哈希

**函数** : `hexmd5`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`data` | `string` | 需要进行hash的内容


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`hash` | `string` | 可读 hash 值

**调用样例**

```poc
local crypto = require("crypto")

print(crypto.hexmd5("1\n"))
```


### SHA1 哈希

**函数** : `sha1`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`data` | `string` | 需要进行hash的内容


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`hash` | `string` | 不可读 hash 值

**调用样例**

```poc
local crypto = require("crypto")

print(crypto.sha1("1\n"))
```

### HEXSHA1 哈希

**函数** : `hexsha1`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`data` | `string` | 需要进行hash的内容


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`hash` | `string` | 可读 hash 值

**调用样例**

```poc
local crypto = require("crypto")

print(crypto.hexsha1("1\n"))
```

### SHA224 哈希

**函数** : `sha224`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`data` | `string` | 需要进行hash的内容


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`hash` | `string` | 不可读 hash 值

**调用样例**

```poc
local crypto = require("crypto")

print(crypto.sha224("1\n"))
```

### HEXSHA224 哈希

**函数** : `hexsha224`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`data` | `string` | 需要进行hash的内容


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`hash` | `string` | 可读 hash 值

**调用样例**

```poc
local crypto = require("crypto")

print(crypto.hexsha224("1\n"))
```

### SHA256 哈希

**函数** : `sha256`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`data` | `string` | 需要进行hash的内容


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`hash` | `string` | 不可读 hash 值

**调用样例**

```poc
local crypto = require("crypto")

print(crypto.sha256("1\n"))
```

### HEXSHA256 哈希

**函数** : `hexsha256`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`data` | `string` | 需要进行hash的内容


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`hash` | `string` | 可读 hash 值

**调用样例**

```poc
local crypto = require("crypto")

print(crypto.hexsha256("1\n"))
```


### SHA384 哈希

**函数** : `sha384`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`data` | `string` | 需要进行hash的内容


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`hash` | `string` | 不可读 hash 值

**调用样例**

```poc
local crypto = require("crypto")

print(crypto.sha384("1\n"))
```

### HEXSHA384 哈希

**函数** : `hexsha384`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`data` | `string` | 需要进行hash的内容


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`hash` | `string` | 可读 hash 值

**调用样例**

```poc
local crypto = require("crypto")

print(crypto.hexsha384("1\n"))
```

### SHA512 哈希

**函数** : `sha512`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`data` | `string` | 需要进行hash的内容


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`hash` | `string` | 不可读 hash 值

**调用样例**

```poc
local crypto = require("crypto")

print(crypto.sha512("1\n"))
```

### HEXSHA512 哈希

**函数** : `hexsha512`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`data` | `string` | 需要进行hash的内容


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`hash` | `string` | 可读 hash 值

**调用样例**

```poc
local crypto = require("crypto")

print(crypto.hexsha512("1\n"))
```

### HMAC 哈希

**函数** : `hmac`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`digestmod` | `string` | 哈希方式 支持`md5`,`sha1`,`sha256`,`sha512`
`message` | `string` | 信息
`key` | `string` | key
`raw` | `bool` | 是否需要`raw`数据，非`raw`数据为`hex`数据,默认`false`返回`hex`数据


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`data` | `string` | 返回HMAC数据
`error` | `string` | 错误信息，HMAC过程中如果出现问题错误信息在这显示

**调用样例**

```poc
local crypto = require("crypto")

print(crypto.hmac("md5", "Hello, world!", "secret", false))
```

### AES | DES 加密数据

**函数** : `encrypt`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`data` | `string` | 待加密的数据
`method` | `string` | 加密的方式 `des-ecb`,`des-cbc`,`aes-cbc`
`key` | `string` | key
`options` | `number` | 数据结果的编码，`0` 为 `hex` 输出, `1` 为 `raw` 输出
`iv` | `string` | 加密，`IV`


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`data` | `string` | 返回加密后的数据
`error` | `string` | 错误信息，加密过程中如果出现问题错误信息在这显示

**调用样例**

```poc
local crypto = require("crypto")

local v,err = crypto.encrypt("AAAAAA", "aes-cbc", "AAAAAAAAAAAAAAAA", 0, "AAAAAAAAAAAAAAAA")
if err then
    error(err)
end
print(v)
```

### AES | DES 解密数据

**函数** : `decrypt`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`data` | `string` | 待解密的数据
`method` | `string` | 解密的方式 `des-ecb`,`des-cbc`,`aes-cbc`
`key` | `string` | key
`options` | `number` | 数据结果的编码，`0` 为 `hex` 输入, `1` 为 `raw` 输入
`iv` | `string` | 解密，`IV`


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`data` | `string` | 返回加密后的数据
`error` | `string` | 错误信息，加密过程中如果出现问题错误信息在这显示

**调用样例**

```poc
local crypto = require("crypto")

local v, err = crypto.encrypt("AAAAAA", "aes-cbc", "AAAAAAAAAAAAAAAA", 1, "AAAAAAAAAAAAAAAA")
-- 加密
if err then
    error(err)
end
print(v)
-- 解密加密过的数据
local d, err = crypto.decrypt(v, "aes-cbc", "AAAAAAAAAAAAAAAA", 1, "AAAAAAAAAAAAAAAA")
if err then
    error(err)
end
print(d)
```