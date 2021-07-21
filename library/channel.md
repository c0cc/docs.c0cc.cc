# channel 通道

### 创建通道

    通道是一种类似于队列一样的结构，等同于 golang 中的 chan

**函数** : `make`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`length` | `number` | channel的长度


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`chan` | `Channel` | Channel对象



**调用样例**

```poc
local chanle = require("channel")

local chan = channel.make(1)

```

### select

    select是类似go语言中，通过select取值的一种方式
    
    该值可以时一个 |<- 分之，配合 default 分之，判断channel中是否有数据可以取到

**函数** : `select`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`params` | `table` | `select` 每个分支的判断条件，该函数是可变参数，每个参数都是table,table组成部分如下

table 参数表

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`op` | `string` | `op` 为操作条件,<-&#124; 为送值到chan,&#124;<- 为从chan内取值，default 为前两种操作都失败的默认操作
`chan` | `channel` | channel操作对象,`op`值为`default`时，该值可以不写，不需要补位
`value` | `all` | `op` 为 <-&#124; 时,该值必须写，送到channel的内容
`func` | `function` | 处理值的内容,`op`为 <-&#124; 则函数参数为`(发送的值)`, `op`为 &#124;<- 则函数参数为`(是否成功取值,值内容)`,`op`为 default 则函数无参数



**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`index` | `number` | 成功处理的分之索引
`value` | `all` | channel中取到的值
`exists` | `bool` | 是否成功取值



**调用样例**

```poc
local channel = require("channel")
local chan = channel.make(2)
channel.select({ "<-|", chan, "hello" })
print(channel.select({ "|<-", chan, function(exists, val)
    print("Func1:", exists, val)
end }, { "default", chan, function(exists, val)
    print("Func:", exists, val)
end }))

print(channel.select({ "|<-", chan, function(exists, val)
    print("Func1:", exists, val)
end }, { "default", chan, function(exists, val)
    print("Func:", exists, val)
end }))

```

### send

    绑定到 make 的 channel 对象的方法
    
    送一个数据到 channel 中

**函数** : `send`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`chan` | `channel` | channel对象自身
`value` | `all` | 送到channel的值


**函数返回**

无


**调用样例**

```poc
local channel = require("channel")

local chan = channel.make(2)
chan:send("hello")

```

### receive

    绑定到 make 的 channel 对象的方法
    
    从 channel 中取一个值
    
!> 注意：函数返回 exists 为 false 的情况是 `channel` 关闭，正常从空 `channel` 取值会导致线程阻塞

**函数** : `receive`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`chan` | `channel` | channel 对象自身


**函数返回**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`exists` | `bool` | 是否成功取到值
`value` | `all` | 从 channel 中取到的值


**调用样例**

```poc
local channel = require("channel")

local chan = channel.make(2)
chan:send("hello")
chan:receive("hello")

```


### close

    绑定到 make 的 channel 对象的方法
    
    关闭 channel
    
!> 注意：被`close`如果从中取值，`exists` 一直为false

**函数** : `close`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`chan` | `channel` | channel 对象自身


**函数返回**

无


**调用样例**

```poc
local channel = require("channel")

local chan = channel.make(2)
chan:send("hello")
chan:receive("hello")
chan:close()
```