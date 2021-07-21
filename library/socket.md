# socket 套接字支持库



### 域名解析

    对域名进行解析返回IP

**函数** : `lookup`

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`domain` | `string` | 需要获取的IP的域名

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`ipaddr` | `string` | 域名解析返回的IP
`err` | `string` | 报错返回信息，如果该值不为空，则result内容为空

**调用样例**

```poc
local socket = require("socket")

local ip, err = socket.lookup("www.baidu.com")

if err ~= nil then
    error(err)
end

print(ip)
```

### 创建一个新的连接

    创建一个新的连接，返回socket对象

**函数** : `new`

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`options` | `table` | 参数设置，目前仅支持tls参数,例如socket.new({ tls = true })

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`sock` | `userdata` | 返回一个连接对象

**调用样例**

```poc
local socket = require("socket")

local sock = socket.new({ tls = true })
```


### 设置超时参数

    为socket对象设置超时参数

**函数** : `timeout`

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`userdata` | `userdata` | 对象自身
`time` | `number` | 设置超时参数(秒)

**函数返回**

无

**调用样例**

```poc
local crypto = require("crypto")

local sock = socket.new({ tls = true })
sock:timeout(1)

```

### 设置servername

    为socket对象设置servername，可通过IP进行https的连接

**函数** : `servername`

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`userdata` | `userdata` | 对象自身
`hostname` | `string` | 设置连接的主机名(服务器获取到的客户端请求的主机名)

**函数返回**

无

**调用样例**

```poc
local socket = require("socket")

local sock = socket.new({ tls = true })
sock:servername("www.baidu.com")
```


### 连接到远程服务器

    连接到远程服务器

**函数** : `connect`

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`userdata` | `userdata` | 对象自身
`type` | `string` | 连接的方式(tcp,udp)
`hostname` | `string` | 主机名
`port` | `string` | 连接端口，可number 可string

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`status` | `bool` | 连接是否成功的状态信息
`err` | `string` | 报错返回信息，如果该值不为空，则status内容为空

**调用样例**

```poc
local socket = require("socket")

local sock = socket.new({ tls = true })

local status, err = sock:connect("tcp", "127.0.0.1", 8080)

if err ~= nil then
    error(err)
end
print(status)
```


### 发送数据到远程服务器

    发送数据到远程服务器

**函数** : `send`

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`userdata` | `userdata` | 对象自身
`data` | `string` | 发送的数据

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`status` | `bool` | 数据是否成功的状态信息

**调用样例**

```poc
local socket = require("socket")

local sock = socket.new({ tls = true })

local status, err = sock:connect("tcp", "127.0.0.1", 8080)

if err ~= nil then
    error(err)
end
local status = sock:send("hello")
print(status)
```



### 从远程服务器读取数据

    从远程服务器读取数据

**函数** : `recv`

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`userdata` | `userdata` | 对象自身
`size` | `number` | 接收数据的缓冲区

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`msg` | `string` | 接受到的信息
`length` | `number` | 接收到信息的长度
`error` | `string` | 接收数据中的报错信息

**调用样例**

```poc
local socket = require("socket")

local sock = socket.new({ tls = true })

local status, err = sock:connect("tcp", "127.0.0.1", 8080)

if err ~= nil then
    error(err)
end
local status = sock:send("hello")
local msg, length, err = sock:recv(1024)
if err ~= nil then
    error(err)
end
print(msg)
```

### 关闭连接

    关闭连接

**函数** : `close`

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`userdata` | `userdata` | 对象自身

**函数返回**

无

**调用样例**

```poc
local socket = require("socket")

local sock = socket.new({ tls = true })

local status, err = sock:connect("tcp", "127.0.0.1", 8080)

sock:close()
```