# coroutine 协程


### 创建 coroutine

    创建 coroutine，返回 coroutine， 参数是一个函数，当和 resume 配合使用的时候就唤醒函数调用

**函数** : `create`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`func` | `function` | 函数


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`coroutine` | `coroutine` | `coroutine`对象


**调用样例**

```poc
co = coroutine.create(
    function(i)
        print(i);
    end
)

```

### 重启 coroutine

    重启 coroutine，和 create 配合使用,负责外部向内传递参数并且将内部yield函数传递出来的内容取到

**函数** : `resume`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`co` | `coroutine` | `coroutine` 对象
`param` | `value` | 多值，传入参数


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`coroutine` | `coroutine` | `coroutine`对象


**调用样例**

```poc
function foo (a)
    print("foo 函数输出", a)
    return coroutine.yield(2 * a) -- 返回  2*a 的值
end
 
co = coroutine.create(function (a , b)
    print("第一次协同程序执行输出", a, b) -- co-body 1 10
    local r = foo(a + 1)
     
    print("第二次协同程序执行输出", r)
    local r, s = coroutine.yield(a + b, a - b)  -- a，b的值为第一次调用协同程序时传入
     
    print("第三次协同程序执行输出", r, s)
    return b, "结束协同程序"                   -- b的值为第二次调用协同程序时传入
end)
       
print("main", coroutine.resume(co, 1, 10)) -- true, 4
print("--分割线----")
print("main", coroutine.resume(co, "r")) -- true 11 -9
print("---分割线---")
print("main", coroutine.resume(co, "x", "y")) -- true 10 end
print("---分割线---")
print("main", coroutine.resume(co, "x", "y")) -- cannot resume dead coroutine
print("---分割线---")
```


### 挂起 coroutine

    挂起 coroutine，将 coroutine 设置为挂起状态，同时向外传递参数

**函数** : `yield`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`co` | `coroutine` | `coroutine` 对象
`param` | `value` | 多值，送出值


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`value` | `value` | `resume`函数送进来的多个值对象


**调用样例**

```poc
function foo (a)
    print("foo 函数输出", a)
    return coroutine.yield(2 * a) -- 返回  2*a 的值
end
 
co = coroutine.create(function (a , b)
    print("第一次协同程序执行输出", a, b) -- co-body 1 10
    local r = foo(a + 1)
     
    print("第二次协同程序执行输出", r)
    local r, s = coroutine.yield(a + b, a - b)  -- a，b的值为第一次调用协同程序时传入
     
    print("第三次协同程序执行输出", r, s)
    return b, "结束协同程序"                   -- b的值为第二次调用协同程序时传入
end)
       
print("main", coroutine.resume(co, 1, 10)) -- true, 4
print("--分割线----")
print("main", coroutine.resume(co, "r")) -- true 11 -9
print("---分割线---")
print("main", coroutine.resume(co, "x", "y")) -- true 10 end
print("---分割线---")
print("main", coroutine.resume(co, "x", "y")) -- cannot resume dead coroutine
print("---分割线---")
```


### 查看coroutine状态

    查看coroutine对象的状态

**函数** : `status`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`coroutine` | `coroutine` | `coroutine`对象


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`status` | `string` | 返回`coroutine`对象的状态，状态有三种：`dead`(死亡)，`suspended`(挂起)，`running`(运行中)


**调用样例**

```poc
co = coroutine.create(
    function(i)
        print(i);
    end
)
print(coroutine.status(co))

```

### 获取当前运行coroutine对象

    线程同时只运行1个,获取到当前运行线程的对象，即掌握主动权的代码块，获取当前线程的对象

**函数** : `running`


**函数参数**

无


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`coroutine` | `coroutine` | 返回当前`coroutine`对象


**调用样例**

```poc
co2 = coroutine.create(
        function()
            for i = 1, 10 do
                print(i)
                if i == 3 then
                    print(coroutine.status(co2))  --running
                    local co1 = coroutine.running()
                    print("status1", coroutine.status(co1))
                end
                coroutine.yield()
            end
        end
)

coroutine.resume(co2) --1
coroutine.resume(co2) --2
coroutine.resume(co2) --3

print(coroutine.status(co2))   -- suspended
print("running1", coroutine.running())

```


### coroutine的另一种包装方式

    查看coroutine对象的状态

**函数** : `status`


**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`func` | `function` | 被包装的对象


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`func` | `coroutine` | 返回函数式`coroutine`对象，参考下面例子


**调用样例**

```poc
co = coroutine.wrap(function(i)
    local r = coroutine.yield(i)
    coroutine.yield(r)
end)

local result = co(1000)
print(result)
result = co(3)
print(result)

-- 输出
-- 10000
-- 3

```