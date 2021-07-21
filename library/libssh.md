# libssh SSH连接支持库


### 开始一个session

**函数** : `session_open`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`hostname` | `string` | 连接的对端主机IP
`port` | `string` | 连接的对端主机端口
`timeout` | `number` | 连接超时参数


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`conn` | `userdata` | 连接成功时返回UserData的连接对象
`err` | `string` | 报错返回信息，如果该值不为空，则result内容为空

**调用样例**

```poc
local libssh = require("libssh")

local conn,err = libssh.session_open("192.168.1.100", 22, 3)
if err ~= nil then
    error("conn error")
end
```

### 获取支持的验证方式(目前只实现了通过对密码的验证，该方式意义不大)

**函数** : `session_open`


**函数参数**

无


**函数返回**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`userdata` | `userdata` | session对象
`authMethod` | `table` | 获取支持的连接方式的名字表,该表为空时获取失败

**调用样例**

```poc
local libssh = require("libssh")

local conn,err = libssh.session_open("192.168.1.100", 22, 3)
if err ~= nil then
    error("conn error")
end

print(conn:userauth_list())
```

### 通过用户名密码验证登陆

**函数** : `userauth_password`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`userdata` | `userdata` | session对象
`username` | `string` | 用于验证的用户名
`password` | `string` | 用于验证的密码

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`state` | `bool` | 连接的状态信息，是否成功
`err` | `string` | 报错返回信息，如果该值不为空，则result内容为空

**调用样例**

```poc
local libssh = require("libssh")

local conn,err = libssh.session_open("192.168.1.100", 22, 3)
if err ~= nil then
    error("conn error")
end

local connect_state, err = conn:userauth_password("root", "password")
if connect_state then
    print("connect ok")
end
```

### 关闭会话

**函数** : `session_close`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`userdata` | `userdata` | session对象

**函数返回**

无

**调用样例**

```poc
local libssh = require("libssh")

local conn,err = libssh.session_open("192.168.1.100", 22, 3)
if err ~= nil then
    error("conn error")
end

conn:session_close()
```

### 打开一个channel

**函数** : `open_channel`


**函数参数**

无

**函数返回**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`userdata` | `userdata` | session对象
`channel` | `userdata` | 打开一个channel
`err` | `string` | 报错返回信息，如果该值不为空，则result内容为空

**调用样例**

```poc
local libssh = require("libssh")

-- 创建一个session
local conn,err = libssh.session_open("192.168.1.100", 22, 3)
if err ~= nil then
    error("conn error")
end

-- 通过账号密码进行验证
local connect_state, err = conn:userauth_password("root", "password")
if not(connect_state) then
    error("connect fail")
end

获取到channel,该channel可以执行命令
local channel, err = conn:open_channel()
```

### 通过channel执行命令

**函数** : `channel_exec`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`userdata` | `userdata` | channel对象
`command` | `string` | 远程执行ssh命令(此处建议使用不卡的命令)

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`output` | `string` | 输出命令执行的结果
`err` | `string` | 报错返回信息，如果该值不为空，则result内容为空

**调用样例**

```poc
local libssh = require("libssh")

-- 创建一个session
local conn,err = libssh.session_open("192.168.1.100", 22, 3)
if err ~= nil then
    error("conn error")
end

通过账号密码进行验证
local connect_state, err = conn:userauth_password("root", "password")
if not(connect_state) then
    error("connect fail")
end

-- 获取到channel,该channel可以执行命令
local channel, err =conn:open_channel()
if err ~= nil then
    error(err)
end

local output, err = channel:channel_exec("id")
if err ~= nil then
    error(err)
end
print(output)
```


### 关闭channel

**函数** : `channel_close`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`userdata` | `userdata` | channel对象

**函数返回**

无

**调用样例**

```poc
local libssh = require("libssh")

-- 创建一个session
local conn,err = libssh.session_open("192.168.1.100", 22, 3)
if err ~= nil then
    error("conn error")
end

-- 通过账号密码进行验证
local connect_state, err = conn:userauth_password("root", "password")
if not(connect_state) then
    error("connect fail")
end

-- 获取到channel,该channel可以执行命令
local channel, err =conn:open_channel()
if err ~= nil then
    error(err)
end

channel:channel_close()
```

