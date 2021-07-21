# 插件格式

插件在创建过程中，有三个函数是必要的

`audit` : 负责任务调度

`assign` : 负责对目标进行测试

`test` : 负责在本地进行测试 

## 创建一个默认的插件

程序提供了快捷创建模版的方式

```bash
➜  build ./node_darwin_amd64 -c xx.poc
          _   _
     /\  | | | |
    /  \ | |_| |__   ___ _ __   __ _
   / /\ \| __| '_ \ / _ \ '_ \ / _  |
  / ____ \ |_| | | |  __/ | | | (_| |
 /_/    \_\__|_| |_|\___|_| |_|\__,_|

[2020-12-16 14:27:48] DEBUG Node: 正在创建模版文件:xx.poc
[2020-12-16 14:27:48] DEBUG Node: 模版文件创建完成

```

模版文件格式大概如下
```poc
local http = require("http")
-- 库导入

function assign(service, param)
    --- 任务调度函数
    -- 该函数返回2个值 (是否进行处理,被处理过的参数)
    -- 被处理的参数会自动进行去重工作
    -- 比如两次插件调用,返回param相同,则除了第一次,后续参数相同的返回参数不会调用审计函数
    ---
    if service == "service" then
        return true, param
    end
end

function audit(param)
    --- 扫描审计函数
    -- 扫描过程中对外发起请求,以及联动操作的动作,对审计结果的上报
    ---

    print(("admin"):md5()) -- admin的md5内容

    local resp = http.get(param)
    if resp.code == 200 then
        -- 研判漏洞，并且上报同时，附带请求响应包
        report_hole("this is vuln", resp)
    end
end

function test()
    -- service检查
    local checkrun, param = assign("service", "https://www.baidu.com")
    if checkrun then
        -- service检查成功则调用审计函数
        audit(param)
    end
end

```

## 插件运行流程

**节点运行**

`assign`检查 -> `audit`

先通过`assign`函数进行`service`的检查,如果确定了扫描的服务为目标服务，返回 2 个值

第一个值是给框架判断是否要调用`audit`审计函数，第二个值是传参数给 `audit` 审计函数


**本地测试**

本地测试的话，框架不进行主动调用 任务调度函数和审计函数，一切操作都是由`test`函数自行完成，可以有一些前置生成参数的流程

具体的`service` 可以参考web `应用管理->应用列表` 中的`service`,编写对应的`service`应用