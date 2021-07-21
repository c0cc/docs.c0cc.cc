# 本地化运行

    为了有更广泛的应用，本框架决定优化本地化运行的方式，增加本地化运行增强模块，实现可以有更广泛的数据接入

## 目录结构

    为了对本地化的增强，第一步就是将对于服务器的资源进行本地化的结构存取
    
    |- node.exe (主程序)
    |- lib      (支持库目录)
    |- static   (静态资源目录)
    |- plugins  (插件目录)

**目录介绍**

`node.exe` 为主程序的代称，实际的名字可以进行随意的修改

`lib` 目录用于存放支持库文件，即自行编写的支持库，使用require语句进行导入，支持后缀为`.poc` 与 `.lua` 的文件的导入

`static` 静态资源的存放，使用 `loadconst` 函数进行加载文件，此处的存放的文件例如爆破的账号密码,对静态资源进行统一的管理与存放

`plugins` 此处文件的名称并重要，只是有个代称，用于存放插件的目录，此处也可以是多个目录，通过`load_plugins`函数对目录中的所有插件进行加载


## 加强模块

    为了加强本地化的运行，主脚本中引入了一个新的模块，名为athena，用于对任务的管理以及对扫描报告的处理


## TaskManager 任务管理结构

### 添加任务

**函数** : `add`

**函数参数** 

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`task` | `Task` | 添加任务对象

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`status` | `bool` | 添加是否成功
`err` | `string` | 错误信息

**调用样例**

```poc
local athena = require("athena")

local taskmgr = athena.TaskManager()

local task = athena.Task()

local status,err = taskmgr:add(task)
-- 显示任务错误信息
if err ~= nil then
    error(err)
end
```

### 任务数量

**函数** : `num`

**函数参数** 

参数名 | 参数类型 | 参数说明
---- | ---- | ----

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`num` | `number` | 任务数量信息
`err` | `string` | 错误信息

**调用样例**

```poc
local athena = require("athena")

local taskmgr = athena.TaskManager()

local task = athena.Task()

local status,err = taskmgr:num(task)
-- 显示任务错误信息
if err ~= nil then
    error(err)
end
```

### 任务ID列表

**函数** : `idlist`

**函数参数** 

参数名 | 参数类型 | 参数说明
---- | ---- | ----

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`ids` | `table` | 任务的ID列表
`err` | `string` | 错误信息

**调用样例**

```poc
local athena = require("athena")

local taskmgr = athena.TaskManager()

local idlist,err = taskmgr:idlist()
-- 显示任务错误信息
if err ~= nil then
    error(err)
end

for _,task_id in ipairs(idlist) do
    print(task_id)
end
```

### 任务列表是否为空

**函数** : `empty`

**函数参数** 

参数名 | 参数类型 | 参数说明
---- | ---- | ----

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`empty` | `bool` | 任务池是否为空
`err` | `string` | 错误信息

**调用样例**

```poc
local athena = require("athena")

local taskmgr = athena.TaskManager()

local empty,err = taskmgr:empty()
-- 显示任务错误信息
if err ~= nil then
    error(err)
end

print(string.format("Empty:%s", empty))
```

### 结束任务

**函数** : `kill`

**函数参数** 

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`task_id` | `string` | 需要结束的任务的ID

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`status` | `bool` | 任务结束是否成功
`err` | `string` | 错误信息

**调用样例**

```poc
local athena = require("athena")

local taskmgr = athena.TaskManager()

local status, err = taskmgr:kill("Task1_ID")
-- 显示任务错误信息
if err ~= nil then
    error(string.format("任务结束失败,错误信息:%s", err))
end

print(string.format("任务结束状态:%s", status))
```

### 任务池工作函数
    
    对任务池内的任务进行清理

**函数** : `pool`

**函数参数** 

参数名 | 参数类型 | 参数说明
---- | ---- | ----


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----


**调用样例**

```poc
local athena = require("athena")

local taskmgr = athena.TaskManager()

taskmgr:pool()
```

### 报告channel
    
    taskmgr中的task，报告统一在此处输出

**函数** : `report`

**函数参数** 

参数名 | 参数类型 | 参数说明
---- | ---- | ----


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`report` | `channel` | 返回的报告，可以使用`channel`模块进行读取


**调用样例**

```poc
local athena = require("athena")

local taskmgr = athena.TaskManager()

local report = taskmgr:report()

channel.select({ "|<-", report, function(exists, val)
    print("Func1:", exists, val)
end }, { "default", report, function(exists, val)
    -- 占位防止卡死
end })
```

## Task 任务结构

### 设置Cookie

**函数** : `set_cookie`

**函数参数** 

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`cookie` | `string` | http请求中的 Cookie 值

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`err` | `string` | 错误信息

**调用样例**

```poc
local athena = require("athena")

local task = athena.Task()

local err  = task:set_cookie("a=bb")
-- 显示任务错误信息
if err ~= nil then
    error(err)
end
```

### 设置UA

**函数** : `set_user_agent`

**函数参数** 

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`User-Agent` | `string` | http请求中的 User-Agent 值

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`err` | `string` | 错误信息

**调用样例**

```poc
local athena = require("athena")

local task = athena.Task()

local err  = task:set_user_agent("Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.114 Safari/537.36")
-- 显示任务错误信息
if err ~= nil then
    error(err)
end
```

### 设置侵入式扫描

    该函数用于侵入式扫描的 flag 的设置
    
**函数** : `set_aggressive`

**函数参数** 

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`aggressive` | `bool` | 侵入式扫描的状态

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`err` | `string` | 错误信息

**调用样例**

```poc
local athena = require("athena")

local task = athena.Task()

local err  = task:set_aggressive(false)
-- 显示任务错误信息
if err ~= nil then
    error(err)
end
```

### 设置扫描超时时间
    
**函数** : `set_timeout`

**函数参数** 

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`timeout` | `string` | 超时时间

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`err` | `string` | 错误信息

**调用样例**

```poc
local athena = require("athena")

local task = athena.Task()

local err  = task:set_timeout("10")
-- 显示任务错误信息
if err ~= nil then
    error(err)
end
```

### 设置禁止扫描的路径
    
**函数** : `set_disallow`

**函数参数** 

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`disallow_path` | `string` | 禁止扫描的路径信息

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`err` | `string` | 错误信息

**调用样例**

```poc
local athena = require("athena")

local task = athena.Task()

-- 禁止扫描退出登录的路径
local err  = task:set_disallow("/logout")
-- 显示任务错误信息
if err ~= nil then
    error(err)
end
```

### 设置共享知识库
    
**函数** : `set_knowbase`

**函数参数** 

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`key` | `string` | 设置的共享知识库名称
`value` | `string` | 设置共享知识库的内容

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`err` | `string` | 错误信息

**调用样例**

```poc
local athena = require("athena")

local task = athena.Task()

-- 设置共享的知识库
local err  = task:set_knowbase("os","windows")
-- 显示任务错误信息
if err ~= nil then
    error(err)
end
```

### 设置扫描的目标

    该内容由插件进行获取并且进行初始化的扫描，所以内容格式的设置由用户自主进行设置
    
**函数** : `set_target`

**函数参数** 

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`target` | `string` | 扫描的目标网站

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`err` | `string` | 错误信息

**调用样例**

```poc
local athena = require("athena")

local task = athena.Task()

-- 设置扫描的目标
local err  = task:set_target("https://www.baidu.com")
-- 显示任务错误信息
if err ~= nil then
    error(err)
end
```

### 设置扫描线程

    该函数用于对同时运行的插件数量的限制，默认为 10
    
**函数** : `set_thread`

**函数参数** 

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`thread` | `int` | 设置线程

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`err` | `string` | 错误信息

**调用样例**

```poc
local athena = require("athena")

local task = athena.Task()

-- 设置扫描的目标
local err  = task:set_thread(10)
-- 显示任务错误信息
if err ~= nil then
    error(err)
end
```

### 设置扫描的插件

    该函数会清空任务的插件池，重新添加插件到插件池中
    
**函数** : `set_plugins`

**函数参数** 

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`thread` | `int` | 设置线程

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`count` | `number` | 成功加载的插件数量
`err` | `string` | 错误信息

**调用样例**

```poc
local athena = require("athena")

local task = athena.Task()

local plugins = athena.laod_plugins("./plugins")
-- 设置扫描的目标
local count, err  = task:set_plugins(plugins)
-- 显示任务错误信息
if err ~= nil then
    error(err)
end

print(string.format("加载插件 %s 个", count))
```

### 添加插件

    添加新的插件到插件池中，该方法不会清空原有的插件池
    
**函数** : `add_plugin`

**函数参数** 

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`plugin` | `userdata` | 添加的插件

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`status` | `bool` | 添加插件是否成功(此处的成功判断是进行类型的检查)
`err` | `string` | 错误信息

**调用样例**

```poc
local athena = require("athena")

local task = athena.Task()

local plugins = athena.laod_plugins("./plugins")
-- 设置扫描的目标
local status, err  = task:add_plugin(plugins[1])
-- 显示任务错误信息
if err ~= nil then
    error(err)
end

```

### 插件数量

    检查任务的插件池中的插件数量
    
**函数** : `plugin_count`

**函数参数** 

参数名 | 参数类型 | 参数说明
---- | ---- | ----

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`count` | `bool` | 任务的数量
`err` | `string` | 错误信息

**调用样例**

```poc
local athena = require("athena")

local task = athena.Task()

local count, err  = task:plugin_count()
-- 显示任务错误信息
if err ~= nil then
    error(err)
end

print(string.format("插件池中的插件数量: %s", count))
```

### 任务ID

    获取任务的ID，此ID为随机分配
    
**函数** : `get_id`

**函数参数** 

参数名 | 参数类型 | 参数说明
---- | ---- | ----

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`taskid` | `string` | 任务的ID
`err` | `string` | 错误信息

**调用样例**

```poc
local athena = require("athena")

local task = athena.Task()

local taskid, err  = task:get_id()
-- 显示任务错误信息
if err ~= nil then
    error(err)
end

print(string.format("任务ID: %s", taskid))
```

### 添加任务到任务池

**函数** : `taskpush`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`service` | `string` | 添加任务的`service`
`param` | `value` | 扫描过程中需要用到的参数
`target` | `string` | 添加扫描任务，任务在扫描中产生的报告上报展示形式(对子域名等扫描挂在哪个域名下面),可空


**函数返回**

无

**调用样例**

```poc
local athena = require("athena")

local task = athena.Task()


task:taskpush("init", "param", "target")
task:taskpush("init", { "param", "param1" }, "target")
task:taskpush("init", { param = "param1" }, "target")
```


## Plugin 插件结构

### 插件名称

**函数** : `name`

**函数参数** 

参数名 | 参数类型 | 参数说明
---- | ---- | ----

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`name` | `string` | 插件的名字
`err` | `string` | 错误信息

**调用样例**

```poc
local athena = require("athena")

local plugins = athena.load_plugins("./plugins")

local plugin = plugins[1]

print(plugin:name())

```


### 插件Hash

    插件为了进行区分，专门设置了任务hash，来校验插件的唯一性，使用md5算法进行hash

**函数** : `hash`

**函数参数** 

参数名 | 参数类型 | 参数说明
---- | ---- | ----

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`hash` | `string` | 插件的Hash
`err` | `string` | 错误信息

**调用样例**

```poc
local athena = require("athena")

local plugins = athena.load_plugins("./plugins")

local plugin = plugins[1]

print(plugin:hash())

```

## 任务池

**函数** : `TaskManager`

    用于创建任务管理函数，主要应对产生多任务的情况，如果没有多任务的情况可以忽略这部分，就当作形式调用就好

**别名** : `TaskMgr`,`TM`,`tm`

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`TaskManager` | `userdata` | 任务管理器模型

**调用样例**

```poc
local athena = require("athena")

local taskmgr = athena.TaskManager()

```

## 创建任务

**函数** : `Task`

    用于创建任务对象，该任务对象是多个线程，运行任务池中的任务

**别名** : `task`

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`Task` | `userdata` | 任务对象

**调用样例**

```poc
local athena = require("athena")

local task = athena.Task()
```

## 加载插件

**加载插件** : `load_plugin`

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`filename` | `string` | 文件名称，通过文件名进行加载插件

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`plugin` | `plugin` | 加载完成的插件

**调用样例**

```poc
local athena = require("athena")

local plugins = athena.load_plugins("./plugins/hello.poc")

```

## 通过字符串加载插件

**加载插件** : `load_plugin_from_str`

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`chunk` | `string` | 插件代码内容
`filename` | `string` | 插件的名称

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`plugin` | `plugin` | 加载完成的插件

**调用样例**

```poc
local athena = require("athena")

local plugins = athena.load_plugin_from_str("a = 123;return _ENV","./plugins/hello.poc")

```

## 加载插件目录

**加载插件** : `load_plugins`

    批量的插件，此处插件仅加载后缀为 .poc 或 .lua 的插件文件，并且仅加载一级文件

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`dir` | `string` | 目录名称，通过目录进行加载插件

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`plugins` | `table` | 加载的插件的列表
`error` | `string` | 加载的错误信息

**调用样例**

```poc
local athena = require("athena")

local plugins = athena.load_plugins("./plugins")

```

 
 
