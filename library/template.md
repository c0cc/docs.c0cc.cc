# 模版支持库


### 创建模版引擎

**函数** : `choose`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`egname` | `string` | 引擎名称，目前仅支持 `mustache`


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`engine` | `userdata` | 引擎对象
`err` | `string` | 报错返回信息，如果该值不为空，则前面都为空


**调用样例**

```poc
local template = require("template")

local mustache, err = template.choose("mustache")
if err then
    error(err)
end
```


### 渲染文本

**函数** : `render`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`userdata` | `userdata` | 对象自身
`templates` | `string` | 模版
`values` | `string` | 渲染值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`renderstring` | `string` | 返回被渲染的字符串
`err` | `string` | 报错返回信息，如果该值不为空，则前面都为空



**调用样例**

```poc
local template = require("template")

local mustache, err = template.choose("mustache")
if err then
    error(err)
end

local values = {name="world"}
local result, err = mustache:render("Hello {{name}}!", values)
if err then
    error(err)
end

if not(result == "Hello world!") then
    error(result)
end

local values = {data = {"one", "two"}}
local result, err = mustache:render("{{#data}} {{.}} {{/data}}", values)
if err then
    error(err)
end
if not(result == " one  two ") then
    error(result)
end
```



### 渲染来自于文件的文本

**函数** : `render_file`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`userdata` | `userdata` | 对象自身
`templates_file` | `string` | 模版文件
`values` | `string` | 渲染值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`renderstring` | `string` | 返回被渲染的字符串
`err` | `string` | 报错返回信息，如果该值不为空，则前面都为空



**调用样例**

```poc
local template = require("template")

local mustache, err = template.choose("mustache")
if err then
    error(err)
end

local values = {name="world"}
local result, err = mustache:render_file("/root/xxx.txt", values)
if err then
    error(err)
end
```
