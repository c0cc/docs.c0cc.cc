# nmap 端口扫描模块

    该模块因扫描验证服务的数据来源与nmap，所以取名叫nmap模块

### 扫描端口

**函数** : `scan`

    为了规避解释器中的设计问题，无法使用多线程，所以决定使用下层的Go实现部分完成扫描
    该函数会对端口进行扫描以及服务的识别，扫描完成后返回一个 table 给用户
    
**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`hostname` | `string` | 主机名
`port` | `string` | 需要扫描的端口
`timeout` | `number` | 超时时间
`thread` | `number` | 扫描线程


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`portlist` | `table` | 扫描完成的端口信息，如果没有扫描到则返回一个空的端口表

> 注意，如果是http服务，将尝试返回服务器的状态码和页面的标题信息

**调用样例**

```poc
local nmap = require("nmap")

function test()
    -- 端口扫描例子 IP，端口表，支持"-,"分隔符，超时时间，扫描线程
    local result = nmap.scan("127.0.0.1", "80", 10, 50)
    -- 输出扫描结果
    for _, service in pairs(result) do
        print(string.rep("-", 20))
        for name, value in pairs(service) do
            print(name, ": ", value)
        end
    end
end

-- 输出结果
          _   _
     /\  | | | |
    /  \ | |_| |__   ___ _ __   __ _
   / /\ \| __| '_ \ / _ \ '_ \ / _  |
  / ____ \ |_| | | |  __/ | | | (_| |
 /_/    \_\__|_| |_|\___|_| |_|\__,_|

[2021-06-24 16:48:53] DEBUG Node: 正在创建运行环境
[2021-06-24 16:48:53] DEBUG Node: 正在载入模块
[2021-06-24 16:48:53] DEBUG Node: 正在装载程序:test_portscan.poc
[2021-06-24 16:48:53] DEBUG Node: 正在运行 test 测试方法
--------------------
Port    :       80
ServiceNmae     :       http
StatusCode      :       502
Title   :       502 Bad Gateway
Url     :       http://127.0.0.1:80
VendorProduct   :       
Version :       
[2021-06-24 16:48:54] DEBUG Node: 运行时间:205.221258ms

```
