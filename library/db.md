# db 数据库支持库

### 打开连接

**函数** : `open`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`dbtype` | `string` | 数据库类型,暂时支持`postgres`,`mongodb`,`sqlite3`,`mssql`,`mysql`,`ql`
`connectString` | `string` | 连接字符串,例如`账号:密码@tcp(IP:端口)/库名` 或sqlite `file:testdb.db?cache=shared&mode=memory`


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`connect` | `DB` | 返回一个连接成功的DB对象
`err` | `string` | 报错返回信息，如果该值不为空，则`connect`内容为空

**调用样例**

```poc
local db = require("db")

local sqlite, err = db.open("sqlite3", "file:testdb.db?cache=shared&mode=memory")
if err then 
    error(err) 
end
sqlite:close()

```

### 运行SQL

    请注意，该方法仅能保证执行sql，并且返回影响行，无法进行查询返回值

**函数** : `exec`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`DB` | `DB` | DB对象
`exec` | `string` | 执行的SQL语句


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `table` | 返回一个表，表包含 `last_insert_id`(最后插入ID),`rows_affected`(受影响的行)
`err` | `string` | 报错返回信息，如果该值不为空，则`result`内容为空

**调用样例**

```poc
local db = require("db")

local sqlite, err = db.open("sqlite3", "file:testdb.db?cache=shared&mode=memory")
if err then 
    error(err) 
end

local _, err = sqlite:exec("CREATE TABLE t (id int, name string);")
if err then
    sqlite:close() 
    error(err) 
end
sqlite:close()
```

### 查询结果

    该方法相对exec方法，可以获取查询的结果集

**函数** : `query`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`DB` | `DB` | DB对象
`query` | `string` | 执行的SQL语句


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `table` | 返回一个表，表包含 `last_insert_id`(最后插入ID),`rows_affected`(受影响的行)
`err` | `string` | 报错返回信息，如果该值不为空，则`result`内容为空

**调用样例**

```poc
local db = require("db")

local sqlite, err = db.open("sqlite3", "file:testdb.db?cache=shared&mode=memory")
if err then 
    error(err) 
end

local result, err = sqlite:query("select * from t;")
if err then 
    error(err) 
end

for i, v in pairs(result.columns) do
    if i == 1 then 
        if not(v == "id") then 
            error("error") 
        end 
    end
    if i == 2 then 
        if not(v == "name") then 
            error("error") 
        end 
    end
end

sqlite:close()
```

### 关闭连接

    关闭一个数据库连接

**函数** : `close`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`DB` | `DB` | DB对象


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`err` | `string` | 返回关闭错误信息

**调用样例**

```poc
local db = require("db")

local sqlite, err = db.open("sqlite3", "file:testdb.db?cache=shared&mode=memory")
if err then 
    error(err) 
end

local err = sqlite:close()
if err then
    error(err)
end
```
