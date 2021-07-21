# string 字符串支持库

### 获取字符ascii码

    可以获取一个字符串内的多个成员的ascii码

**函数** : `byte`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`data` | `string` | 源数据
`start` | `number` | 起始位置
`end` | `number` | 结束位置


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`ascii` | `number` | 根据参数不同，可能会返回多个`number`值

**调用样例**

```poc
-- 首先定义一个字符串
local str = "012abcd"
print("str = "..str)

-- 使用常规方式
print("\nafter string.byte(str,1,4)")
print(string.byte(str,1,4))

-- 使用另一种表现方式
print("\nafter str:byte(1,4)")
print(str:byte(1,4))

-- 使用负数索引
print("\nafter str:byte(-2,-1)")
print(str:byte(-2,-1))

-- 当参数i大于j时
print("\nafter str:byte(2,1)")
print(str:byte(2, 1))

-- 当索引无效时
print("\nafter str:byte(2000,1000000)")
print(str:byte(2000,1000000))
```


### ascii转字符串

    可以同时将多个ascii转成字符串拼接到一起

**函数** : `byte`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`char` | `number` | ascii码，多个值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`data` | `string` | 多个ascii转成字符串

**调用样例**

```poc
print(string.char(48,49,50))

```

### 转小写字符串


**函数** : `lower`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`string` | `string` | 需要转小写的字符串


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`data` | `string` | 已经转换成小写的字符串

**调用样例**

```poc
print(string.lower("AAA"))

```

### 转大写字符串


**函数** : `upper`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`string` | `string` | 需要转大写的字符串


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`data` | `string` | 已经转换成大写的字符串

**调用样例**

```poc
print(string.upper("aaa"))

```

### 去除两侧特定的字符串

    去除的字符串会被拆开，单个的trim

**函数** : `trim`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`string` | `string` | 两侧有脏数据的字符串
`trim` | `string` | 需要去掉字符串


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`data` | `string` | 已经去掉脏数据的字符串

**调用样例**

```poc
print(string.trim("abxxxxbb", "ab"))
-- 输出 xxxx

```

### 去除左侧特定的字符串

    去除的字符串会被拆开，单个的trim

**函数** : `ltrim`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`string` | `string` | 左侧有脏数据的字符串
`trim` | `string` | 需要去掉字符串


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`data` | `string` | 已经去掉脏数据的字符串

**调用样例**

```poc
print(string.ltrim("abxxxxbb", "ab"))
-- 输出 xxxxbb

```

### 去除右侧特定的字符串

    去除的字符串会被拆开，单个的trim

**函数** : `rtrim`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`string` | `string` | 右侧有脏数据的字符串
`trim` | `string` | 需要去掉字符串


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`data` | `string` | 已经去掉脏数据的字符串

**调用样例**

```poc
print(string.rtrim("abxxxxbb", "ab"))
-- 输出 abxxxx

```

### 起始字符串判断

    判断一个字符串的开始是否是另外一个字符串

**函数** : `starts`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`string` | `string` | 想要判断的字符串
`starts` | `string` | 用于对比的字符串


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`ok` | `bool` | 是否`string`是以`starts`开头

**调用样例**

```poc
print(string.starts("abxxxxbb", "ab"))
-- 输出 true

```


### 结束字符串判断

    判断一个字符串的结束是否是另外一个字符串

**函数** : `ends`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`string` | `string` | 想要判断的字符串
`ends` | `string` | 用于对比的字符串


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`ok` | `bool` | 是否`string`是以`ends`结尾

**调用样例**

```poc
print(string.ends("abxxxxbb", "bb"))
-- 输出 true

```

### 包含字符串判断

    判断一个字符串是否包含另外一个字符串

**函数** : `contains`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`string` | `string` | 想要判断的字符串
`value` | `string` | 用于对比的字符串


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`ok` | `bool` | 是否`string`包含`value`

**调用样例**

```poc
print(string.contains("aabbc","bb"))
-- 输出 true

```

### 字符串转hex编码

    对字符串进行hex编码

**函数** : `hex`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`string` | `string` | 需要编码的字符串


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `string` | 编码后的字符串

**调用样例**

```poc
print(string.hex("aabbc"))

```

### hex字符串解码

    对hex字符串进行解码

**函数** : `unhex`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`string` | `string` | 需要解码的字符串


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `string` | 解码后的字符串
`err` | `string` | 错误信息

**调用样例**

```poc
print(string.unhex("313233"))

```

### 字符串进行MD5哈希

    对字符串进行哈希计算

**函数** : `md5`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`string` | `string` | 需要哈希的字符串


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `string` | 哈希后的值

**调用样例**

```poc
print(string.md5("admin"))
-- 输出 21232f297a57a5a743894a0e4a801fc3

```

### 字符串进行分割

    分割字符串

**函数** : `split`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`string` | `string` | 需要分割的字符串
`split` | `string` | 分割的字符串
`count` | `number` | 分割的次数


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `table` | 分割后的字符串表

**调用样例**

```poc

print(string.split("admin","d"))
-- 或
print(("admin"):split("d"))

```

### 字符串替换内容

    替换字符串中的指定内容

**函数** : `replace`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`string` | `string` | 需要替换的字符串
`oldstring` | `string` | 旧的字符串
`newstring` | `string` | 替换成的新的字符串
`count` | `number` | 替换的次数


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`result` | `string` | 替换后的字符串

**调用样例**

```poc

print(string.replace("admin", "dm", "aa"))

```

### 计算字符串出现的次数

    计算一个字符串出现在另外一个字符串中的次数

**函数** : `count`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`string` | `string` | 原字符串
`substring` | `string` | 短字符串(用于统计的字符串)


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`count` | `number` | 字符串出现的次数

**调用样例**

```poc

print(string.replace("adminaaa", "a"))

```


### 计算字符串的长度

    计算字符串的长度

**函数** : `len`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`string` | `string` | 用于计算长度的字符串


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`len` | `number` | 字符串的长度

**调用样例**

```poc

print(string.len("adminaaa"))

```


### 查找字符串

    查找字符串索引，此处因为较为复杂，建议编写过程中多进行测试

**函数** : `find`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`string` | `string` | 源字符串
`parrent` | `string` | 查找的表达式
`init` | `number` | 可选,起始位置
`plain` | `bool` | 可选,`true`为文本匹配,`false`为表达式匹配


`parrent`在`plain`默认，即`false`的情况下，支持如下表达式

表达式 | 含义
---- | ----
`.` | 任意字符
`%s` | 空白符
`%S` | `%s` 反向集合
`%p` | 标点
`%P` | `%p` 反向集合
`%c` | 控制字符
`%C` | `%c` 反向集合
`%d` | 数字
`%D` | `%d` 反向集合
`%x` | 十六进制数
`%X` | `%x` 反向集合
`%z` | 代表0的字符
`%Z` | `%z` 反向集合
`%a` | 字母
`%A` | `%a` 反向集合
`%l` | 小写字母
`%L` | `%l` 反向集合
`%u` | 大写字母
`%U` | `%u` 反向集合
`%w` | 字母数字
`%W` | `%w` 反向集合
`*` | 匹配前面指定的 0 或多个同类字符， 尽可能匹配更`长`的符合条件的字串
`+` | 匹配前面指定的 1 或多个同类字符， 尽可能匹配更`长`的符合条件的字串
`-` | 匹配前面指定的 0 或多个同类字符， 尽可能匹配更`短`的符合条件的字串


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`startindex` | `number` | 查询结果集的开始
`endindex` | `number` | 查询结果集的结束
`result` | `string` | 查询结果的内容，此result可能会有多个值，根据匹配的模式不同

**调用样例**

```poc

local s = "abc \"it's a cat\""
local index, ends, _, q = string.find(s, "it")
print(s:sub(index, ends))

print( ("\"hello\" \"hello\""):find('"(.+)"') )  ----输出 1 15 hello" "hello
print( ("\"hello\" \"hello\""):find('"(.-)"') )  ----输出 1 7 hello

```



### 格式化字符串


**函数** : `format`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`string` | `string` | 源字符串,源字符串包含的占位符在下方
`value` | `obj` | 多个value值，用于format


占位符 | 说明 | 举例 | 输出
---- | ---- | ---- | ----
`%v` | 相应值的默认格式                         | string.format("%v", "hello") | hello
`%%` | 字面上的百分号，并非值的占位符             | string.format("%%")          | %
`%t` | `true` 或 `false`                      | string.format("%t", true)    | true
`%b` | 二进制表示                              | string.format("%b", 5)       | 101
`%c` | 相应Unicode码点所表示的字符               | string.format("%c", 0x4E2D)  | 中
`%d` | 十进制表示                               | string.format("%d", 0x12)   | 18
`%o` | 八进制表示                               | string.format("%d", 10)     | 12
`%q` | 单引号围绕的字符字面值，安全地转义          | string.format("%q", 0x4E2D)  | '中'
`%x` | 十六进制表示，字母形式为小写 a-f           | string.format("%x", 13)      | d
`%X` | 十六进制表示，字母形式为大写 A-F           | string.format("%x", 13)      | D
`%U` | Unicode格式：U+1234，等同于 "U+%04X"     | string.format("%U", 0x4E2D)  | U+4E2D
`%e` | 科学计数法，例如 -1234.456e+78           | string.format("%e", 10.2)    | 1.020000e+01
`%E` | 科学计数法，例如 -1234.456E+78           | string.format("%e", 10.2)    | 1.020000E+01
`%f` | 有小数点而无指数，例如 123.456            | string.format("%f", 10.2)    | 10.200000
`%g` | 根据情况选择 %e 或 %f 以产生更紧凑的（无末尾的0）输出 | string.format("%g", 10.20)    | 10.2
`%G` | 根据情况选择 %E 或 %f 以产生更紧凑的（无末尾的0）输出 | string.format("%G", 10.20+2i) | (10.2+2i)
`%s` | 输出字符串表示（string类型或[]byte)       | string.format("%s", "Athena")  | Athena
`%q` | 双引号围绕的字符串，安全地转义             | string.format("%q", "Athena")  | "Athena"
`%x` | 十六进制，小写字母，每字节两个字符          | string.format("%x", "golang")  | 676f6c616e67
`%X` | 十六进制，大写字母，每字节两个字符          | string.format("%X", "golang")  | 676F6C616E67


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`startindex` | `number` | 查询结果集的开始
`endindex` | `number` | 查询结果集的结束
`result` | `string` | 查询结果的内容，此result可能会有多个值，根据匹配的模式不同

**调用样例**

```poc

print(string.format("Hello %s", "Athena"))

```


### 重复字符串

    将一个字符串复制拼接 ，repeat

**函数** : `rep`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`string` | `string` | 字符串
`count` | `number` | 重复的次数


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`string` | `string` | 重复拼接后的字符串

**调用样例**

```poc

print(string.rep("=",3))
-- 输出 ===

```


### 反转字符串

    将一个字符串进行反转

**函数** : `reverse`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`string` | `string` | 字符串


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`string` | `string` | 反转后的字符串

**调用样例**

```poc

print(string.reverse("123"))
-- 输出 321

```

### 匹配字符串

    只寻找源字串str中的第一个配对. 参数init可选, 指定搜寻过程的起点, 默认为1。
    在成功配对时, 函数将返回配对表达式中的所有捕获结果; 如果没有设置捕获标记, 则返回整个配对字符串. 当没有成功的配对时, 返回nil。

**函数** : `match`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`string` | `string` | 字符串
`parrent` | `string` | 匹配的表达式，表达式可参见 `find` 方法中的表达式文档
`init` | `number` | 搜寻的起始位置


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`string` | `string` | 匹配到的字符串

**调用样例**

```poc

print(string.match("I have 2 questions for you.", "%d+ %a+"))
-- 输出 2 questions

print(string.format("%d, %q", string.match("I have 2 questions for you.", "(%d+) (%a+)")))
-- 输出 2, "questions"

```


### 字符串截取

    字符串截取

**函数** : `sub`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`string` | `string` | 字符串
`start` | `number` | 开始索引
`ends` | `number` | 结束索引，默认`-1`,到结束位置


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`string` | `string` | 截取后多的字符串

**调用样例**

```poc

local sourcestr = "prefix--runoobgoogletaobao--suffix"
print("\n原始字符串", string.format("%q", sourcestr))

```



### 在字符串中替换

    在字符串中替换

**函数** : `gsub`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`string` | `string` | 字符串
`findString` | `string` | 查找的字符串,不同于`replace`方法，支持表达式，表达式参考`find`方法文档
`replaceString` | `string` | 替换的字符串
`num` | `number` | 替换的次数，默认全部替换


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`string` | `string` | 替换后的字符串

**调用样例**

```poc

print(string.gsub("aaaa","a","z",3))
-- 输出 zzza    3

```

### 编码

    部分编码方法，部分编码解码方式名字有重复缩写，看个人习惯，容错率高点

**函数** : `encode`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`string` | `string` | 字符串
`code` | `string` | 编码的方式,支持`base64`,`b64`,`base32`,`b32`,`hex`,`zlib`,`flate`,`deflate`,`md5`,`sha1`,`sha224`,`sha256`,`url`


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`string` | `string` | 编码后的字符串
`err` | `string` | 编码报错

**调用样例**

```poc
local s = "admin"
print(s:md5())

print(string.md5(s))
```

### 解码

    部分解码方法，部分编码解码方式名字有重复缩写，看个人习惯，容错率高点

**函数** : `decode`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`string` | `string` | 字符串
`code` | `string` | 解码的方式,支持`base64`,`b64`,`base32`,`b32`,`hex`,`zlib`,`flate`,`deflate`,`url`


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`string` | `string` | 解码后的字符串
`err` | `string` | 解码报错

**调用样例**

```poc
local s = "admin"
print(s:md5())

print(string.md5(s))
```

### pack

    二进制编码，该函数正在实现中

**函数** : `pack`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`string` | `string` | pack的字符串
`...` | `value` | pack的内容...支持多个值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `string` | 生成好的二进制字符串
`err` | `string` | 编码的错误信息

**调用样例**

```poc

print(string.pack("b", 90))
-- 输出 
Z
```

### unpack

    二进制解码

**函数** : `unpack`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`string` | `string` | pack的字符串
`value` | `string` | 已经被编码过的数据


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`...` | `value` | 解码的多个值
`length` | `number` | 解码的数量

**调用样例**

```poc
print(string.unpack("b", string.pack("b", 90)))

-- 输出
90
```

### packsize

    二进制编码长度测试，测试pack字符串的长度

**函数** : `packsize`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`format` | `string` | pack的字符串



**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`length` | `number` | pack字符串产生的内容的长度

**调用样例**

```poc
print(string.packsize("bbb"))

-- 输出
3
```
