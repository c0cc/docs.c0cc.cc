# 内置对象

## 内置函数
**knowbase**

别名:`KB`,`knowbase`,`KnowBase`

变量作用

    用于存储一些共享内容，例如用户自定义的shell代码,为了躲避查杀软件
    
    存储一些例如系统版本，系统类型等共享信息，暂时其他类型信息还未标准化，但是shell信息有标准化
    
    shell信息在可以进行稳定的激进扫描的情况下，建议getshell，扫描页面已对用户警示
    
    KB["shell"]["asp"]      ASP shell代码
    KB["shell"]["asppass"]  ASP shell密码
    KB["shell"]["aspx"]     ASPXshell代码
    KB["shell"]["aspxpass"] ASPXshell密码
    KB["shell"]["php"]      PHP shell代码
    KB["shell"]["phppass"]  PHP shell密码
    KB["shell"]["jsp"]      JSP shell代码
    KB["shell"]["jsppass"]  JSP shell密码
    

!> 请注意,`jsp` 实际上是 `CUSTOM` 模式的shell


**aggressive**

别名:`aggressive`,`A`

变量作用
    
    侵入式扫描
    
    该变量是服务器用户添加任务的过程中，用户对目标站点不关心是否产生破坏性行为
    
    该选项模式下，可以直接在服务器留存shell文件，可以对服务器进行破坏性测试


## 函数

### 设置元表

    为指定的table设置元表metatable，如果metatable为nil则取消table的元表，当metatable有__metatable字段时，将触发错误

**函数** : `setmetatable`

    
**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `value` | 用于获取元表的对象
`metatable` | `table` | 元表


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `value` | 返回设置元表的对象

**调用样例**

```poc
print(setmetatable(1,{}))
```   

### 获取元表

    返回指定对象的元表(若object的元表.__metatable项有值，则返回object的元表.__metatable的值)，当object没有元表时将返回nil

**函数** : `getmetatable`

    
**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `value` | 用于获取元表的对象


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`metatable` | `table` | 元表的内容

**调用样例**

```poc
print(getmetatable(1))
```



### 遍历表

    功能：允许程序遍历表中的每一个字段，返回下一索引和该索引的值。
    参数：table：要遍历的表
    index：要返回的索引的前一索中的号，当index为nil[]时，将返回第一个索引的值，当索引号为最后一个索引或表为空时将返回nil
    注：可以用next(t)来检测表是否为空(此函数只能用于以数字索引的表与ipairs相类似)

**函数** : `next`

    
**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`table` | `table` | 用于遍历的表
`index` | `value` | 索引


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`index` | `value` | 索引，当前索引传入next第二参数，会获取下一对 `key`-`value`
`value` | `value` | 值内容

**调用样例**

```poc
local t = {"hello","world"}
print(next(t,1))
```


### 比较内容

    检测v1是否等于v2，此函数不会调用任何元表的方法

**函数** : `rawequal`

    
**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`v1` | `value` | 用于比较的值1
`v2` | `value` | 用于比较的值2


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `bool` | 比较的值 `true` 或 `false`


**调用样例**

```poc
print(rawequal(1, 2))

```


### 设置内容到表

    设置表中指定索引的值，此函数不会调用任何元表的方法，此函数将返回table

**函数** : `rawset`
    
**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`table` | `table` | 表
`key` | `value` | 设置到表中的`key`
`value` | `value` | 设置到表中的`value`


**函数返回**

无

**调用样例**

```poc
t={"1","cash"}
rawset(t,1,"aaaa")

```

### 从表中获取内容

    获取表中指定索引的值，此函数不会调用任何元表的方法，成功返回相应的值，当索引不存在时返回nil
    本函数只能用于以数字索引访问的表 如：t={"1","cash"}

**函数** : `rawget`

    
**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`table` | `table` | 表
`key` | `value` | 表中的`key`


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `value` | 返回的值


**调用样例**

```poc
t={"1","cash"}
print(rawget(t,1))

```


### unpack 解table到参数表

    返回指定表的索引的值,i为起始索引，j为结束索引
    本函数只能用于以数字索引访问的表,否则只会返回nil 如：t={"1","cash"}
    
**函数** : `unpack`

    
**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `table` | 用于`unpack`的表


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `value` | 返回的多值，参见说明


**调用样例**

```poc
select(2,"a","b","c")

```

### select

    当index为数字将返回所有index大于index的参数:如：select(2,"a","b") 返回 "b"
    当index为"#"，则返回参数的总个数(不包括index)

**函数** : `select`
    
**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`index` | `string` 或 `number` | 功能
`value` | `value` | 传入的参数


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `value` | 返回的多值，参见说明


**调用样例**

```poc
select(2,"a","b")

```

### GC 垃圾回收

    垃圾回收

**函数** : `collectgarbage`


**函数参数**

无

**函数返回**

无

**调用样例**

```poc
collectgarbage()
```


### xpcall 在保护模式下调用函数

    发生的错误将不会反射给调用者

**函数** : `xpcall`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`func` | `function` | 函数对象
`errfunc` | `function` | 函数运行报错处理函数 function(errmsg) end


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`status` | `bool` | 运行状态是否成功
`err` | `string` | 运行失败此处是`string` 类型的错误信息


**调用样例**

```poc
function add()
    return a + b
end

function errmsg(v1)
    print("111",v1)
end

local status,val = xpcall(add,errmsg)
if status then
    print(val)
end

```

### pcall 在保护模式下调用函数

    发生的错误将不会反射给调用者

**函数** : `pcall`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`func` | `function` | 函数对象
`args` | `value` | 函数参数，可变参数


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`status` | `bool` | 运行状态是否成功
`val` | `value` | 如果运行成功，此处是多个函数返回值，运行失败此处是`string` 类型的错误信息


**调用样例**

```poc

function add(a,b)
    return a + b
end

local status,val = pcall(add,1,2)
if status then
    print(val)
end

```



### 获取变量类型

    获取程序变量的类型

**函数** : `type`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `value` | 需要判断的内容


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`type` | `string` | 变量的类型

**调用样例**

```poc
print(type(1))
```

### loadstring 加载程序

    通过字符串加载程序

**函数** : `loadstring`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`code` | `string` | 代码内容
`chunkname` | `string` | 代码名称


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`fn` | `function` | 加载完成的函数对象
`err` | `string` | 返回加载错误信息 

**调用样例**

```poc
local fn = loadstring("return 1+1")
```


### loadfile 加载程序

    读取文件加载程序

**函数** : `loadfile`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`filename` | `string` | 通过程序文件进行加载程序


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`fn` | `function` | 加载完成的函数对象
`err` | `string` | 返回加载错误信息 

**调用样例**

```poc
local value = loadfile("/root/text.poc")
```

### 加载程序

    从reader加载程序

**函数** : `load`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`reader` | `function` | 加载程序的`reader`


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`fn` | `function` | 函数对象 
`err` | `string` | 返回加载错误信息 

**调用样例**

```poc
-- 此处只是示例，可以通过打开文件的方式，通过reader函数进行代码读取
flag = true
function reader()
    if flag then
        flag = false
        return "return add"
    end
end
value = load(reader)()
print(value(1, 2))
```
### dofile 从文件加载程序

    从文件中加载程序，程序文件的路径可以自由定义

**函数** : `dofile`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`filename` | `string` | 程序文件的路径


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`module` | `value` | 根据运行程序的文件最后的`return`,决定返回的内容 

**调用样例**

```poc
local env = dofile("/root/test.poc")

```


### 错误

    一段程序在运行过程中产生了无法挽回的后果，报错退出，error函数执行后程序会自行报错退出

**函数** : `error`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`error` | `string` | 报错的错误信息
`level` | `number` | 报错的错误等级


**函数返回**

无

**调用样例**

```poc
error("mdzz")
```


### 断言

    一段一句运行在经过断言的时候，一定传入一个 判断时为 true 的值，不然引发一个严重错误并且退出程序

**函数** : `assert`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `bool` | 用于断言的值
`error` | `string` | 如果断言失败,则抛出该异常


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `value` | 返回传入值

**调用样例**

```poc
assert(2 == 1 + 1, "表达式不正确")
```


### 输出到屏幕

    输出一段内容到控制台

**函数** : `print`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `value` | 多参数


**函数返回**

无

**调用样例**

```poc
print("hello world")
```



### 转换成文本

**函数** : `tostring`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `value` | 需要转换的值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `string` | 转换成字符串对象

**调用样例**

```poc
print(tostring(1111))
```


### 转换成数字

**函数** : `tonumber`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `string` 或 `number` | 需要转换的值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `number` | 转换成数字对象

**调用样例**

```poc
print(tonumber("3.14"))
```


### 导入模块

**函数** : `require`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`modulename` | `string` | 模块名称


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`module` | `module` | 模块对象

**调用样例**

```poc
local base64 = require("base64")
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
taskpush("init", "param", "target")
taskpush("init", { "param", "param1" }, "target")
taskpush("init", { param = "param1" }, "target")
```


### 上报扫描记录

    在web界面展示中标记为绿色,该值为后续渗透中提供一些基础信息

**函数** : `report_note`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`msg` | `string` | 扫描产生的上报信息
`senddata` | `string`或`http_response` | 扫描过程中发送出去的验证包,用于展示给用户
`recvdata` | `string` | 扫描过程中发送验证包的返回值


**函数返回**

无

**调用样例**

```poc
report_note("this is note message", "senddata", "recvdata")
```


### 上报报告低危

    在web界面展示中标记为蓝色,该值为一些低危信息,例如信息泄漏

**函数** : `report_info`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`msg` | `string` | 扫描产生的上报信息
`senddata` | `string`或`http_response` | 扫描过程中发送出去的验证包,用于展示给用户
`recvdata` | `string` | 扫描过程中发送验证包的返回值


**函数返回**

无

**调用样例**

```poc
report_info("this is info message", "senddata", "recvdata")
```



### 上报报告中危

    在web界面展示中标记为黄色,该值为一些中危信息,例如容易产生对站点有影响但是不至于导致站点被直接攻陷的漏洞,例如Ddos.XSS 等

**函数** : `report_warn`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`msg` | `string` | 扫描产生的上报信息
`senddata` | `string`或`http_response` | 扫描过程中发送出去的验证包,用于展示给用户
`recvdata` | `string` | 扫描过程中发送验证包的返回值


**函数返回**

无

**调用样例**

```poc
report_warn("this is info message", "senddata", "recvdata")
```


### 上报报告高危

    在web界面展示中标记为红色,该值为一些高危信息,例如直接导致站点被攻陷或极有可能打通边界的问题

**函数** : `report_hole`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`msg` | `string` | 扫描产生的上报信息
`senddata` | `string`或`http_response` | 扫描过程中发送出去的验证包,用于展示给用户
`recvdata` | `string` | 扫描过程中发送验证包的返回值


**函数返回**

无

**调用样例**

```poc
report_hole("this is info message", "senddata", "recvdata")
```

### 上报Shell

    提交Shell到服务器，展示在对应的任务中展示

**函数** : `report_shell`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`url` | `string` | Shell 地址
`passwordd` | `string` | Shell 密码,可空
`type` | `string` | Shell类型,支持`asp`,`aspx`,`php`,`jsp`,可空


**函数返回**

无

**调用样例**

```poc
report_shell("https://www.baidu.com/xxx.php", "passwd", "php")
```

### 加载网络支持库


**函数** : `loadlib`

    该函数在本地测试过程中，同require一样，功能为对本地支持库的加载
    
    该函数在扫描过程中，通过本地的支持库管理，联通到服务器的支持库，并且进行加载

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`libname` | `string` | 网络支持库的名称
`lib` | `module` | 返回加载好的网络支持库对象


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`module` | `module` | 模块对象

**调用样例**

```poc
local const = loadconst("constname", "default const value")

```


### 加载静态资源

**函数** : `loadconst`

    该函数在本地测试过程中，会处理两个参数，第一参数为加载的静态常量名称
    函数在扫描过程中仅处理第一参数，即通过const名称从服务器拉取相应的文件
    该函数存在的意义为可动态升级部分资源，例如 子域名爆破中 子域名字典


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`constname` | `string` | 网络加载静态常量的名称
`defaultvalue` | `module` | 静态处理资源


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`constvalue` | `string` | 返回加载好的静态常量

**调用样例**

```poc
local const = loadconst("constname", "default const value")

```
