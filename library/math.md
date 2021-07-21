# math 数学支持库

### 绝对值

**函数** : `abs`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `number` | 值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `number` | 返回绝对值

**调用样例**

```poc
local math = require("math")
print(math.abs(-15))
-- 输出 15

```
    
    
### 反余弦函数

**函数** : `acos`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `number` | 值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `number` | 返回反余弦值

**调用样例**

```poc
local math = require("math")
print(math.acos(0.5))
-- 输出 1.04719755

```

    

### 反正弦函数

**函数** : `asin`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `number` | 值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `number` | 返回反正弦值

**调用样例**

```poc
local math = require("math")
print(math.asin(0.5))
-- 输出 0.52359877

```
    
    
### x/y的反正切值

**函数** : `atan2`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `number` | 值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `number` | 返回 `x/y` 的反正切值

**调用样例**

```poc
local math = require("math")
print(math.atan2(90.0, 45.0))
-- 输出 1.10714871

```
    

### 反正切函数

**函数** : `atan`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `number` | 值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `number` | 返回 反正切值

**调用样例**

```poc
local math = require("math")
print(math.atan(0.5))
-- 输出 0.463647609

```


### 不小于x的最大整数

**函数** : `ceil`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `number` | 值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `number` | 返回不小于x的最大整数

**调用样例**

```poc
local math = require("math")
print(math.ceil(5.8))
-- 输出 6

```


### 双曲线余弦函数

**函数** : `cosh`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `number` | 值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `number` | 返回双曲线余弦函数

**调用样例**

```poc
local math = require("math")
print(math.cosh(0.5))
-- 输出 1.276259652

```


### 余弦函数

**函数** : `cos`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `number` | 值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `number` | 返回余弦值

**调用样例**

```poc
local math = require("math")
print(math.cos(0.5))
-- 输出 0.87758256

```
    

### 弧度转角度

**函数** : `deg`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `number` | 值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `number` | 返回弧度转角度

**调用样例**

```poc
local math = require("math")
print(math.deg(math.pi))
-- 输出 180

```


### 计算以e为底x次方值

**函数** : `exp`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `number` | 值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `number` | 返回计算以e为底x次方值

**调用样例**

```poc
local math = require("math")
print(math.exp(2))
-- 输出 2.718281828

```


### 不大于x的最大整数

**函数** : `floor`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `number` | 值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `number` | 返回不大于x的最大整数

**调用样例**

```poc
local math = require("math")
print(math.floor(5.6))
-- 输出 5

```


### 取模运算

**函数** : `fmod`(`mod`)


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `number` | 值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `number` | 返回取模运算

**调用样例**

```poc
local math = require("math")
print(math.mod(14, 5))
-- 输出 4

```

### frexp

    把双精度数val分解为数字部分（尾数）和以2为底的指数n，即val=x*2n

**函数** : `fmod`(`mod`)


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `number` | 值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `number` | 返回frexp

**调用样例**

```poc
local math = require("math")
print(math.frexp(10.0))
-- 输出  0.625    4

```


### ldexp

    计算value * 2的n次方

**函数** : `fmod`(`mod`)


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `number` | 值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `number` | 返回ldexp

**调用样例**

```poc
local math = require("math")
print(math.ldexp(10.0, 3))
-- 输出  80 = 10 * (2 ^3)

```


### 计算以10为基数的对数

**函数** : `log10`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `number` | 值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `number` | 返回以10为基数的对数

**调用样例**

```poc
local math = require("math")
print(math.log10(100))
-- 输出 2

```

### 计算一个数字的自然对数

**函数** : `log`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `number` | 值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `number` | 返回一个数字的自然对数

**调用样例**

```poc
local math = require("math")
print(math.log(2.71))
-- 输出 0.9969

```


### 取得参数中最大值

**函数** : `max`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `number` | 多个值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `number` | 返回参数中最大值

**调用样例**

```poc
local math = require("math")
print(math.max(2.71, 100, -98, 23))
-- 输出 100

```


### 取得参数中最小值

**函数** : `min`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `number` | 多个值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `number` | 返回参数中最小值

**调用样例**

```poc
local math = require("math")
print(math.min(2.71, 100, -98, 23))
-- 输出 -98

```

### 把数分为整数和小数

**函数** : `modf`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `number` | 值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `number` | 整数
`value1` | `number` | 小数

**调用样例**

```poc
local math = require("math")
print(math.modf(15.98))
-- 输出 15    98

```


### 得到x的y次方

**函数** : `pow`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `number` | 值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `number` | 返回 得到x的y次方

**调用样例**

```poc
local math = require("math")
print(math.pow(2, 5))
-- 输出 32

```


### 角度转弧度

**函数** : `rad`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `number` | 值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `number` | 返回 角度转弧度

**调用样例**

```poc
local math = require("math")
print(math.rad(180))
-- 输出 3.14159265358

```


### 获取随机数

**函数** : `random`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `number` | 值的范围开始
`value1` | `number` | 值的范围结束


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `number` | 返回 随机数

**调用样例**

```poc
local math = require("math")
print(math.random(1, 100))
-- 输出 获取1-100的随机数

```


### 设置随机数种子

    在使用math.random函数之前必须使用此函数设置随机数种子

**函数** : `randomseed`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `number` | 随机数种子


**函数返回**

无

**调用样例**

```poc
local math = require("math")
math.randomseed(os.time())


```


### 双曲线正弦函数

**函数** : `sinh`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `number` | 值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `number` | 返回 双曲线正弦值

**调用样例**

```poc
local math = require("math")
print(math.sinh(0.5))
-- 输出 0.5210953

```

### 正弦函数

**函数** : `sin`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `number` | 值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `number` | 返回 正弦值

**调用样例**

```poc
local math = require("math")
print(math.sin(math.rad(30)))
-- 输出 0.5

```

### 开平方函数

**函数** : `sqrt`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `number` | 值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `number` | 返回 开平方值

**调用样例**

```poc
local math = require("math")
print(math.sqrt(16))
-- 输出 4

```


### 双曲线正切函数

**函数** : `tanh`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `number` | 值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `number` | 返回 双曲线正切值

**调用样例**

```poc
local math = require("math")
print(math.tanh(0.5))
-- 输出 0.46211715

```

### 正切函数

**函数** : `tan`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`value` | `number` | 值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `number` | 返回 正切值

**调用样例**

```poc
local math = require("math")
print(math.tan(0.5))
-- 输出 0.5463024

```



### 获取随机字符串

    该函数用于生成一个随机的字符串

**函数** : `randomstr`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`string` | `string` | 可空，随机的字符串选择的字符串列表，默认:大小写字母数字下划线
`length` | `number` | 生成的长度,默认8


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `string` | 返回的随机字符串

**调用样例**

```poc
local math = require("math")

print(math.randomstr())

print(math.randomstr(8))

print(math.randomstr("12345",8))

-- 如果需要一个随机的文件名

print(string.format("_%s.jpg", math.randomstr()))

```
