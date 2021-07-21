# http 请求支持库

### 请求响应封装对象
    
    一个正常成功的请求会返回一个封装好的http响应对象
    
    响应后面单独带了s，例如 headers,requests,responses,是为了进行整体判断
    
    requests,responses还有单独的作用，在进行请求报问报文上报的时候，传入response对象会自动取走这两个属性

**响应对象属性**

属性名 | 属性类型 | 属性说明
---- | ---- | ----
`code` | `number` | 请求响应状态码
`err` | `string` | 请求响应状态码为0的情况下为请求失败，err中会有报错信息，请求成功的情况下该值为nil
`header` | `table` | 响应头内容 格式{ key = {values} } ,外层字典，value为列表的结构，原因是key使用多个value，例如set-cookie
`cookie` | `table` | cookie内容,格式为{ key = value },value不允许一个key对应多个值
`body` | `string` | 响应内容的正文,字符串
`headers` | `string` | 后面带了s,则一般为字符串结构,响应头内容全部拼接为字符串的方式
`requests` | `strings` | 请求完整报文
`responses` | `string` | 响应内容整体的输出,该值一般用于扫描结果上报,方便后续对该类漏洞的整理和反馈处理

### 持续会话

**函数** : `session`

    session是指保留服务端发送回来的cookie，并且在下一次请求中带上，维持请求cookie
    
    需要注意的是，session中的参数仅支持在session创建过程中进行设置，不支持单独设置到

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`options` | `table` | 请求参数的设置，目前支持3个参数，```{ jump = true , timeout = 30 , ip="127.0.0.1:80"}```

option参数

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`jump` | `bool` | 请求302是否自动响应跳转
`timeout` | `number` | 请求超时时间,单位:秒
`ip` | `string` | 连接的IP地址以及端口 例如:"127.0.0.1:8080"，这边设置的ip端口，下方请求就会都发到这里

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`session` | `userdata` | session对象，session对象有request, get, post, put, delete, options方法(下方请求方法)

**调用样例**

```poc
local http = require("http")
local session = http.session({ jump = true , timeout = 30})
local response = session:get("https://www.baidu.com", {  })
print(response.code)
if response.code ~= 0 then -- 如果请求成功，输出响应正文
    print(response.body)
end
```


### 自定义请求

**函数** : `request`

    向web服务器发起一个自定义请求

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`url` | `string` | 请求地址
`options` | `table` | 请求参数的设置，下方options设置为table中的参数

option参数

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`method` | `string` | 请求方法,该参数独立是为了设置的方便，可修改为非常规名字
`header` | `table` |  支持 header={a="bb",b={"aa","bb","cc"}} ,即，一个名字多个value
`ua` | `string` | 请求User-Agent
`body` | `string` | 请求正文,仅支持字符串，其他形式请先转换
`raw` | `string` | 请求raw内容，从 GET / HTTP1.1 起一直到结束，使用该选项则不解析其他参数，但是User-Agent例外，因为有全局统一参数，不进行手动设置优先全局
`ip` | `string` | 该字段可以指定创建连接的IP地址,例如:"127.0.0.1:8080",通过session对象请求，该字段由session控制
`jump` | `bool` | 该字段可以指定是否自动处理跳转请求,3xx,通过session对象请求，该字段由session控制
`timeout` | `number` | 该字段可以指定连接超过多长时间为超时异常,单位:秒,通过session对象请求，该字段由session控制


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`response` | `response` | 参考文档上方的响应对象

**调用样例**

```poc
local http = require("http")
local response = http.request("https://www.baidu.com", { method = "GET"})
print(response.code)
if response.code ~= 0 then
    print(response.body)
end
```

### GET

**函数** : `get`

    向web服务器发起一个get请求

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`url` | `string` | 请求地址
`options` | `table` | 请求参数的设置，下方options设置为table中的参数

option参数

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`header` | `table` |  支持 header={a="bb",b={"aa","bb","cc"}} ,即，一个名字多个value
`ua` | `string` | 请求User-Agent
`body` | `string` | 请求正文,仅支持字符串，其他形式请先转换
`raw` | `string` | 请求raw内容，从 GET / HTTP1.1 起一直到结束，使用该选项则不解析其他参数，但是User-Agent例外，因为有全局统一参数，不进行手动设置优先全局
`ip` | `string` | 该字段可以指定创建连接的IP地址,例如:"127.0.0.1:8080",通过session对象请求，该字段由session控制
`jump` | `bool` | 该字段可以指定是否自动处理跳转请求,3xx,通过session对象请求，该字段由session控制
`timeout` | `number` | 该字段可以指定连接超过多长时间为超时异常,单位:秒,通过session对象请求，该字段由session控制


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`response` | `response` | 参考文档上方的响应对象

**调用样例**

```poc
local http = require("http")
local response = http.get("https://www.baidu.com", { })
print(response.code)
if response.code ~= 0 then
    print(response.body)
end
```


### POST

**函数** : `post`

    向web服务器发起一个post请求

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`url` | `string` | 请求地址
`options` | `table` | 请求参数的设置，下方options设置为table中的参数

option参数

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`header` | `table` |  支持 header={a="bb",b={"aa","bb","cc"}} ,即，一个名字多个value
`ua` | `string` | 请求User-Agent
`body` | `string` | 请求正文,仅支持字符串，其他形式请先转换
`raw` | `string` | 请求raw内容，从 GET / HTTP1.1 起一直到结束，使用该选项则不解析其他参数，但是User-Agent例外，因为有全局统一参数，不进行手动设置优先全局
`ip` | `string` | 该字段可以指定创建连接的IP地址,例如:"127.0.0.1:8080",通过session对象请求，该字段由session控制
`jump` | `bool` | 该字段可以指定是否自动处理跳转请求,3xx,通过session对象请求，该字段由session控制
`timeout` | `number` | 该字段可以指定连接超过多长时间为超时异常,单位:秒,通过session对象请求，该字段由session控制


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`response` | `response` | 参考文档上方的响应对象

**调用样例**

```poc
local http = require("http")
local response = http.post("https://www.baidu.com", {body="aabbcc=1234"})
print(response.code)
if response.code ~= 0 then
    print(response.body)
end
-- 注意: post方法与其他方法不同,自动填充了 Content-Type 头为 application/x-www-form-urlencoded 如果您的需要不同,请在header中设置
```


### PUT

**函数** : `put`

    向web服务器发起一个put请求

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`url` | `string` | 请求地址
`options` | `table` | 请求参数的设置，下方options设置为table中的参数

option参数

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`header` | `table` |  支持 header={a="bb",b={"aa","bb","cc"}} ,即，一个名字多个value
`ua` | `string` | 请求User-Agent
`body` | `string` | 请求正文,仅支持字符串，其他形式请先转换
`raw` | `string` | 请求raw内容，从 GET / HTTP1.1 起一直到结束，使用该选项则不解析其他参数，但是User-Agent例外，因为有全局统一参数，不进行手动设置优先全局
`ip` | `string` | 该字段可以指定创建连接的IP地址,例如:"127.0.0.1:8080",通过session对象请求，该字段由session控制
`jump` | `bool` | 该字段可以指定是否自动处理跳转请求,3xx,通过session对象请求，该字段由session控制
`timeout` | `number` | 该字段可以指定连接超过多长时间为超时异常,单位:秒,通过session对象请求，该字段由session控制


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`response` | `response` | 参考文档上方的响应对象

**调用样例**

```poc
local http = require("http")
local response = http.put("https://www.baidu.com", {body = "awdefsgrt"})
print(response.code)
if response.code ~= 0 then
    print(response.body)
end
```


### DELETE

**函数** : `delete`

    向web服务器发起一个delete请求

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`url` | `string` | 请求地址
`options` | `table` | 请求参数的设置，下方options设置为table中的参数

option参数

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`header` | `table` |  支持 header={a="bb",b={"aa","bb","cc"}} ,即，一个名字多个value
`ua` | `string` | 请求User-Agent
`body` | `string` | 请求正文,仅支持字符串，其他形式请先转换
`raw` | `string` | 请求raw内容，从 GET / HTTP1.1 起一直到结束，使用该选项则不解析其他参数，但是User-Agent例外，因为有全局统一参数，不进行手动设置优先全局
`ip` | `string` | 该字段可以指定创建连接的IP地址,例如:"127.0.0.1:8080",通过session对象请求，该字段由session控制
`jump` | `bool` | 该字段可以指定是否自动处理跳转请求,3xx,通过session对象请求，该字段由session控制
`timeout` | `number` | 该字段可以指定连接超过多长时间为超时异常,单位:秒,通过session对象请求，该字段由session控制


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`response` | `response` | 参考文档上方的响应对象

**调用样例**

```poc
local http = require("http")
local response = http.delete("https://www.baidu.com/aabbx.txt", { })
print(response.code)
if response.code ~= 0 then
    print(response.body)
end
```



### OPTIONS

**函数** : `options`

    向web服务器发起一个options请求

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`url` | `string` | 请求地址
`options` | `table` | 请求参数的设置，下方options设置为table中的参数

option参数

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`header` | `table` |  支持 header={a="bb",b={"aa","bb","cc"}} ,即，一个名字多个value
`ua` | `string` | 请求User-Agent
`body` | `string` | 请求正文,仅支持字符串，其他形式请先转换
`raw` | `string` | 请求raw内容，从 GET / HTTP1.1 起一直到结束，使用该选项则不解析其他参数，但是User-Agent例外，因为有全局统一参数，不进行手动设置优先全局
`ip` | `string` | 该字段可以指定创建连接的IP地址,例如:"127.0.0.1:8080",通过session对象请求，该字段由session控制
`jump` | `bool` | 该字段可以指定是否自动处理跳转请求,3xx,通过session对象请求，该字段由session控制
`timeout` | `number` | 该字段可以指定连接超过多长时间为超时异常,单位:秒,通过session对象请求，该字段由session控制


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`response` | `response` | 参考文档上方的响应对象

**调用样例**

```poc
local http = require("http")
local response = http.options("https://www.baidu.com/aabbx.txt", { })
print(response.code)
```
