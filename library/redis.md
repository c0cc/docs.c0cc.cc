# redis Redis连接支持库


### 打开redis连接

**函数** : `open`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`connectaddr` | `string` | 连接的对端主机IP端口，例如 `127.0.0.1:6379`
`db` | `number` | 连接的对端主机端口


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`conn` | `userdata` | 连接成功时返回UserData的连接对象
`err` | `string` | 报错返回信息，如果该值不为空，则result内容为空

**调用样例**

```poc
local redis = require("redis")

local conn, err = redis.open("127.0.0.1:6379", 0)
if err then
    error(err)
end
```




### 执行redis命令

**函数** : `exec`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`command` | `string` | 连接的对端主机IP端口，例如 `127.0.0.1:6379`
`data` | `table` | 设置参数的内容


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`conn` | `userdata` | 返回的信息
`err` | `string` | 报错返回信息，如果该值不为空，则result内容为空

**调用样例**

```poc
local redis = require("redis")

local conn, err = redis.open("127.0.0.1:6379",0)
if err then
    error(err)
end

local reply, err = conn:exec("SET",{"KKK", "abcdef"})
if err then
    error(err)
end

print(reply)
```




### 关闭redis连接

**函数** : `close`


**函数参数**

无


**函数返回**

无

**调用样例**

```poc
local redis = require("redis")

local conn, err = redis.open("127.0.0.1:6379", 0)
if err then
    error(err)
end

conn:close()
```