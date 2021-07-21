# 系统支持库


### 获取程序启动时间

    获取程序从启动到现在的时间

**函数** : `clock`


**函数参数**

无


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`clock` | `number` | 获取一个程序启动之后到当前的时间,单位:秒

**调用样例**

```poc
local os = require("os")
print(os.clock())
```


### 对比两个时间的差值

**函数** : `difftime`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`currenttime` | `string` | 当前时间
`pretme` | `string` | 以前的时间


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`difft` | `number` | 时间差值，单位:秒

**调用样例**

```poc
-- 奥运会的时间
local tab = {year=2008, month=8, day=8, hour=20}
local pretime = os.time(tab)
print(os.date("08 Olympic Games time is %x", pretime))

-- 现在的时间
local timetable = os.date("*t"); 
local nowtime = os.time(timetable)
print(os.date("now time is %c", nowtime))

local difft = os.difftime(nowtime, pretime);

print("from 08 Olympic Games to now cost time "..difft.."s");
```


### 执行命令

    注意，该方法不会将程序执行的结果返回给程序，只会返回一个状态

**函数** : `execute`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`command` | `string` | 执行的命令


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`runcode` | `number` | 运行代码，`1`为运行出错,`0`为运行成功

**调用样例**

```poc
local os = require("os")

print(os.execute("pwd"))
```

### 程序退出

    注意，运行该方法后，程序立即退出

**函数** : `exit`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`exitcode` | `number` | 程序退出代码,默认为`0`,正常退出


**函数返回**

无

**调用样例**

```poc
local os = require("os")

os.exit(1)
```


### 日期

**函数** : `date`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`formatstring` | `string` | 格式化字符串
`time` | `time` | 传入一个time对象进行格式化,可空


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `string` | 格式化后的字符串

**调用样例**

```poc
-- 奥运会的时间
local tab = {year=2008, month=8, day=8, hour=20}
local pretime = os.time(tab)
print(os.date("08 Olympic Games time is %x", pretime))


local timetable = os.date("*t"); 
local nowtime = os.time(timetable)
print(os.date("now time is %c", nowtime))
```


### 获取环境变量

**函数** : `getenv`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`name` | `string` | 根据名称获取环境变量的内容


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `string` | 返回环境变量的内容或`nil`

**调用样例**

```poc
local os = require("os")

print(os.getenv("PATH"))
```


### 删除文件

**函数** : `remove`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`name` | `string` | 要删除的文件名


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`status` | `bool` | 删除成功为`true`,失败为`nil`
`err` | `string` | 如果文件删除失败，`err` 为错误信息

**调用样例**

```poc
local os = require("os")

local status,err = os.remove("/root/aaa.txt")
if not(status) then
    print("文件删除失败:", err)
else
    print("文件删除成功")
end
```

### 设置环境变量

    该方式设置的环境变量并不是直接设置到系统中，不会保存到系统中，只是在当前环境中

**函数** : `setenv`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`key` | `string` | 设置环境变量的键
`value` | `string` | 设置环境变量的值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`status` | `bool` | 环境设置成功为`true`,失败为`nil`
`err` | `string` | 如果环境设置失败，`err` 为错误信息

**调用样例**

```poc
local os = require("os")

local status,err = os.setenv("AA","BBBB")
if err ~= nil then
    error(err)
end
print("环境设置成功")
```


### 获取一个临时文件名

    该方式获取的了一个临时文件，并且删除了文件，取了一个临时文件名

**函数** : `tmpname`


**函数参数**

无

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`filename` | `string` | 获取到的临时文件名

**调用样例**

```poc
local os = require("os")

local filename = os.tmpname()
print(filename)

```
