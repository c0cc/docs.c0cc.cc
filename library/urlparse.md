# URL解析库


### 解析URL

**函数** : `parse`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`url` | `string` | 解析的字符串内容


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`schema` | `string` | 协议 例如:http
`hostname` | `string` | 主机名 例子:www.baidu.com
`port` | `string` | 端口 例如:8088
`path` | `string` | 路径 例如:/path
`querymap` | `table` | 请求的映射 例如 { a = "b", c = "d"}
`err` | `string` | 报错返回信息，如果该值不为空，则前面都为空



**调用样例**

```poc
local urlparse = require("urlparse")

local schema, hostname, port, path, querymap, err = urlparse.parse("https://www.baidu.com:8088/path?a=b&c=d")
if err ~= nil then
    error(err)
end
```




### URL拼接

**函数** : `join`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`baseurl` | `string` | 拼接的基础URL
`joinurl` | `string` | 拼接的附加URL


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `string` | 拼接后的URL
`err` | `string` | 报错返回信息，如果该值不为空，则前面都为空


**调用样例**

```poc
local urlparse = require("urlparse")

local schema, hostname, port, path, querymap, err = urlparse.parse("https://www.baidu.com:8088/path?a=b&c=d")
if err ~= nil then
    error(err)
end
```
