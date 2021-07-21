# io 输入/输出 支持库


### 打开文件

**函数** : `open`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`filename` | `string` | 打开的文件名
`mode` | `string` | 打开的模式，默认r,可选参数如下

mode 参数

模式 | 模式说明
---- | ---- 
`r` | 以只读方式打开文件，该文件必须存在。
`w` | 打开只写文件，若文件存在则文件长度清为0，即该文件内容会消失。若文件不存在则建立该文件。
`a` | 以附加的方式打开只写文件。若文件不存在，则会建立该文件，如果文件存在，写入的数据会被加到文件尾，即文件原先的内容会被保留。（EOF符保留）
`r+` | 以可读写方式打开文件，该文件必须存在。
`w+` | 打开可读写文件，若文件存在则文件长度清为零，即该文件内容会消失。若文件不存在则建立该文件。
`a+` | 与a类似，但此文件可读可写
`b` | 二进制模式，如果文件是二进制文件，可以加上b
`+` | `+`号表示对文件既可以读也可以写


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`file` | `file` | 返回的文件信息
`err` | `string` | 报错返回信息，如果该值不为空，则`file`内容为空
`errno` | `number` | 错误代码

**调用样例**

```poc
local io = require("io")
local f,err,errno = io.open("/root/aaa.txt")
if err then
    error(err)
end
f:close()
```


### 关闭文件

**函数** : `close`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`file` | `file` | 打开的文件对象


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`bool` | `bool` | 关闭是否成功

**调用样例**

```poc
local io = require("io")
local f,err,errno = io.open("/root/aaa.txt")
if err then
    error(err)
end
io.close(f)
```


### 设置默认输出文件

    设置默认输出后，运行io.write(content) 时，会写入到默认文件中

**函数** : `output`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`file` | `file`或`string` | 打开的文件对象或文件路径,如果文件不存在会创建文件


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`file` | `file` | 返回文件对象

**调用样例**

```poc
local io = require("io")
local f,err,errno = io.open("/root/aaa.txt")
if err then
    error(err)
end
io.output(f)

io.close(f)
```

### 设置默认输入文件

    设置默认输出后，运行io.read() 时，会从默认文件中读取

**函数** : `input`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`file` | `file`或`string` | 打开的文件对象或文件路径


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`file` | `file` | 返回文件对象

**调用样例**

```poc
local io = require("io")
local f = io.input("/root/aaa.txt")

io.close(f)
```


### 缓冲区写入

    将缓冲区内的数据写入到文件中

**函数** : `flush`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`file` | `file` | 打开的文件对象


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`file` | `file` | 返回文件对象

**调用样例**

```poc
local io = require("io")
local f,err,errno = io.open("/root/aaa.txt")
if err then
    error(err)
end
f:write("hello")
io.flush(f)

io.close(f)
```

### 按行读取

    打开指定的文件filename为读模式并返回一个迭代函数,每次调用将获得文件中的一行内容,当到文件尾时，将返回nil,并自动关闭文件。

**函数** : `lines`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`filename` | `string` | 打开指定文件并且返回一个迭代函数 


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`iter` | `func` | 返回的迭代函数

**调用样例**

```poc
local io = require("io")
for line in io.lines("main.lua") do
　　print(line)
end
```


### 获取一个临时文件句柄

    获取一个临时文件句柄，程序结束时自动删除

**函数** : `tmpfile`


**函数参数**

无 


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`file` | `file` | 获取一个临时文件的句柄
`err` | `string` | 获取文件的错误情况

**调用样例**

```poc
local io = require("io")
local f,err = io.tmpfile()
if err ~= nil then
    error(err)
end

```

### 写入数据

    写入数据到文件对象中

**函数** : `write`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`file` | `file` | 文件对象 
`content` | `string` | 写入的文件数据 


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`ok` | `bool` | 写入是否成功，`true`或`nil`
`err` | `string` | 错误信息
`errno` | `number` | 错误代码

**调用样例**

```poc
local io = require("io")
local f,err,errno = io.open("/root/aaa.txt", "w")
if err then
    error(err)
end
f:write("hello")
f:close()
```


### 读取数据

    从文件中读取数据

**函数** : `read`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`file` | `file` | 文件对象 
`mode` | `string` 或 `number` | 读取模式,`*n`:读取一个数字并且返回,`*a`:读取整个文件,`*l`(默认):读取下一行,文件结束返回`nil`,`number`:按长度读取,并且在文件结束时返回nil


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `string` | 读取到的内容或`nil` 

**调用样例**

```poc
local io = require("io")
local f,err,errno = io.open("/root/aaa.txt")
if err then
    error(err)
end
local content = f:read(1024)
print(content)
f:close()
```


### 运行命令并且读写

    运行命令，打开一个句柄，根据参数不同来进行读写内容，完成对命令的后续交互式操作

**函数** : `popen`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`cmd` | `string` | 运行的命令 
`mode` | `string` | 模式 `r`(默认): 读取运行输出的内容,`w`:模拟后续操作，mode只能是两种状态选其一


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`file` | `file` | 返回的`file`对象 
`err` | `string` | 命令执行错误的错误内容 

**调用样例**

```poc
local io = require("io")
local f,err = io.popen("whoami")
if err ~= nil then
    error(err)
end
print(f:read("*a"))
f:close()
```

### 检测文件对象可用

    检测一个文件对象是否可用

**函数** : `type`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`file` | `file` | 被检测的文件对象 


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `string` | 如果不是`file`对象,返回`nil`，关闭的文件对象返回`closed file`,正常文件对象返回`file` 

**调用样例**

```poc
local io = require("io")
local f,err,errno = io.open("/root/aaa.txt")
if err then
    error(err)
end
print(io.type(f))
f:close()
```
