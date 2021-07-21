# lfs 本地文件支持库

    该模块提供了本地访问的能力，原因是后续可能要支持该环境的本地化，通过目录进行加载插件
    
    在此留存一个接口，方便后续本地化插件，用户自行进行资源的加载，可能会用得到
    
    服务器插件都会经过严格审核，不会随便访问本地文件，服务器自身如果想通过测试环境对用户文件系统扫描大可不必通过这种方式

### 获取文件属性

    此函数在内部使用stat
    
    因此，如果给定的文件路径是符号链接，则将其跟随（如果它指向另一个链接，则该链将被递归地跟随）
    
    并且该信息是关于它所引用的文件的。 要获取有关链接本身的信息，请参见lfs.symlinkattributes函数。

**函数** : `attributes`

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`filepath` | `string` | 文件路径
`attr` | `string` | 可空，设置返回指定的的文件属性，文件属性表来自于下方

属性表 

属性名 | 属性说明
---- | ---- 
`dev` | 在Unix系统上，这表示inode所在的设备。 在Windows系统上，表示包含文件的磁盘的驱动器号
`ino` | 在Unix系统上，这表示inode编号。 在Windows系统上，这没有任何意义
`mode` | 代表相关保护模式的字符串,值可以是 file(文件), directory(目录), link(链接), socket(套接字), named pipe(命名管道), char device(字符设备), block device(块设备) 或 other(其他)
`nlink` | 文件的硬链接数
`uid` | 所有者的用户标识（仅Unix，在Windows上始终为0）
`gid` | 所有者的组标识（仅Unix，在Windows上始终为0）
`rdev` | 在Unix系统上，代表特殊文件inode的设备类型。 在Windows系统上代表与dev相同
`access` | 最后访问时间
`modification` | 上次数据修改时间
`change` | 上次文件状态更改的时间
`size` | 文件大小，以字节为单位
`permissions` | 文件权限字符串
`blocks` | 为文件分配的块（仅Unix）
`blksize` | 最佳文件系统I/O块大小（仅Unix）

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`attr` | `string`或`table` | 如果参数中第二参数设置了指定的参数，如果该参数2不设置，则返回一个包含上方参数的`table`
`err` | `string` | 文件属性获取失败的时候返回错误值

**调用样例**

```poc
local lfs = require("lfs")
local attr, err = lfs.attributes("/root")
if err then
    error(err)
end

for k, v in pairs(attr):
    print(k, v)
```



### 切换目录

    切换当前环境所在目录

**函数** : `chdir`

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`path` | `string` | 将当前工作目录更改为给定路径


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`status` | `bool` | 切换是否成功
`err` | `string` | 切换不成功的错误信息

**调用样例**

```poc
local lfs = require("lfs")
local status, err = lfs.chdir("C:\\")
if err then
    error(err)
end

print(status)
```

### 获取当前环境目录

    获取当前工作目录

**函数** : `currentdir`

**函数参数**

无

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`path` | `bool` | 获取到的当前环境目录
`err` | `string` | 获取不成功的错误信息

**调用样例**

```poc
local lfs = require("lfs")
local path, err = lfs.currentdir()
if err then
    error(err)
end

print(path)
```


### 创建目录

    创建目录

**函数** : `mkdir`

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`dirname` | `string` | 需要创建的目录


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`status` | `bool` | 目录创建是否成功 , `true` 或 `nil`
`err` | `string` | 出错原因

**调用样例**

```poc
local lfs = require("lfs")
local status, err = lfs.mkdir("C:\\AA")
if err then
    error(err)
end

print(status)
```



### 创建链接

    创建链接

**函数** : `link`

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`old` | `string` | 文件名称
`new` | `string` | 链接到的位置
`symlink` | `bool` | 创建硬链接，默认flase,可选参数


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`status` | `bool` | 链接文件创建是否成功 `true`或`nil`
`err` | `string` | 出错原因

**调用样例**

```poc
local lfs = require("lfs")
local status, err = lfs.link("/root/aaa.bin", "/root/bbb.bin", true)
if err then
    error(err)
end

print(status)
```

### 删除目录

    删除目录

**函数** : `rmdir`

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`dirname` | `string` | 需要删除的目录


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`status` | `bool` | 目录删除是否成功,`true` 或 `nil`
`err` | `string` | 出错原因

**调用样例**

```poc
local lfs = require("lfs")
local status, err = lfs.mkdir("C:\\AA")
if err then
    error(err)
end

print(status)
```


### 设置文件时间

    设置文件的访问和修改时间

**函数** : `touch`

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`filename` | `string` | 需要修改时间的文件
`atime` | `number` | 访问时间(时间戳) 可选,默认当前时间
`mtime` | `number` | 修改时间(时间戳) 可选,默认和atime一致


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`status` | `bool` | 目录删除是否成功,`true` 或 `nil`
`err` | `string` | 出错原因

**调用样例**

```poc
local lfs = require("lfs")
local status, err = lfs.touch("/root/aaa.txt")
if err then
    error(err)
end
if status then
    print("set time ok")
end

```


### 获取文件属性

    与lfs.attributes相同，除了它获取有关链接本身（而不是它所引用的文件）的信息。 
    
    它还添加了一个 target 字段，其中包含符号链接指向的文件名。 
    
    在Windows上，此功能尚不支持链接，其他与lfs.attributes相同。

**函数** : `symlinkattributes`

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`filepath` | `string` | 文件路径
`attr` | `string` | 可空，设置返回指定的的文件属性，文件属性表来自于下方

属性表 

属性名 | 属性说明
---- | ---- 
`dev` | 在Unix系统上，这表示inode所在的设备。 在Windows系统上，表示包含文件的磁盘的驱动器号
`ino` | 在Unix系统上，这表示inode编号。 在Windows系统上，这没有任何意义
`mode` | 代表相关保护模式的字符串,值可以是 file(文件), directory(目录), link(链接), socket(套接字), named pipe(命名管道), char device(字符设备), block device(块设备) 或 other(其他)
`nlink` | 文件的硬链接数
`uid` | 所有者的用户标识（仅Unix，在Windows上始终为0）
`gid` | 所有者的组标识（仅Unix，在Windows上始终为0）
`rdev` | 在Unix系统上，代表特殊文件inode的设备类型。 在Windows系统上代表与dev相同
`access` | 最后访问时间
`modification` | 上次数据修改时间
`change` | 上次文件状态更改的时间
`size` | 文件大小，以字节为单位
`permissions` | 文件权限字符串
`blocks` | 为文件分配的块（仅Unix）
`blksize` | 最佳文件系统I/O块大小（仅Unix）
`target` | 链接文件指向的真实文件

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`attr` | `string`或`table` | 如果参数中第二参数设置了指定的参数，返回为指定的参数值，如果未设置，则返回一个`table` 包含上方所有属性
`err` | `string` | 文件属性获取失败的时候返回错误值

**调用样例**

```poc
local lfs = require("lfs")
local attr, err = lfs.symlinkattributes("/root")
if err then
    error(err)
end

for k, v in pairs(attr):
    print(k, v)
```




### 获取目录中的文件

    遍历目录,该函数仅对当前目录进行遍历，不对子目录中的文件进行遍历

**函数** : `dir`

**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`dirname` | `string` | 需要遍历的目录，如果不存在则报错

!> 请注意，此处需要提前使用其他函数确定目录的存在，否则会直接导致程序报错退出，可尝试`attributes`

**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`func` | `function` | 通过调用该函数,传入参数为`dir_obj` ，每次调用可以或得下一个目录名称，没有下一个目录的时候，返回`nil`
`dir_obj` | `userdata` | 数据对象

**调用样例**

```poc
local lfs = require("lfs")

local func, dir_obj = lfs.dir("/root")
while true do
    local filename = func(dir_obj)
    if filename ~= nil then
        print(filename)
    else
        break
    end
end
```
