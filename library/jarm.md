# jarm TLS指纹模块

    来源于 https://github.com/salesforce/jarm
    该模块利用服务器对于不同加密版本的请求之间的差异，来对服务器的指纹进行识别
    使用该模块的原因是对恶意服务器进行指纹的标记，可以用于实现恶意服务器的扫描与发现，准确率还是比较高的

### 扫描端口

**函数** : `fingerprint`

    该函数为生成指纹
    
**函数参数**

参数名 | 参数类型 | 参数说明
---- | ---- | ----
`hostname` | `string` | 主机名
`port` | `number` | 连接的端口
`retries` | `number` | 重试次数,客户端每次会2秒的超时时间进行指纹的尝试，通过重试次数来弥补网络的缺陷


**函数返回**

返回值 | 返回类型 | 返回值说明
---- | ---- | ----
`fp` | `string` | 指纹信息

> 需要注意的是，如果指纹信息全为 0 表示识别失败

**调用样例**

```poc
local jarm = require("jarm")

function test()
    print(jarm.fingerprint("8.210.253.122", 443))
end


-- 输出结果
-- 识别失败的指纹
-- 00000000000000000000000000000000000000000000000000000000000000

-- 识别成功的指纹
-- 07d14d16d21d21d07c42d41d00041d24a458a375eef0c576d23a7bab9a9fb1
```

**其他常见C2**

| C2/RED TEAM TOOL |      SSL IMPLEMENTATION TESTED      |                           JARM HASH                            |                    LINK TO TOOL                  |
|---------|------------------------------|----------------------------------------------------------------|--------------------------------------------------|
| Mythic  | python 3 w/aiohttp 3 | 2ad2ad0002ad2ad00042d42d000000ad9bf51cc3f5a1e29eecb81d0c7b06eb | https://github.com/its-a-feature/Mythic          |
| Metasploit ssl listener | ruby 2.7.0p0 | 07d14d16d21d21d00042d43d000000aa99ce74e2c6d013c745aa52b5cc042d | https://github.com/rapid7/metasploit-framework |
| Metasploit ssl listener | ruby | 07d14d16d21d21d07c42d43d000000f50d155305214cf247147c43c0f1a823 | https://github.com/rapid7/metasploit-framework |
| Cobalt Strike | Java 11 | 07d14d16d21d21d07c42d41d00041d24a458a375eef0c576d23a7bab9a9fb1 | https://www.cobaltstrike.com/ |
| Merlin | go 1.15.2 linux/amd64 | 29d21b20d29d29d21c41d21b21b41d494e0df9532e75299f15ba73156cee38 | https://github.com/Ne0nd0g/merlin |
| Deimos | go 1.15.2 linux/amd64 with github.com/gorilla/websocket package | 00000000000000000041d00000041d9535d5979f591ae8e547c5e5743e5b64 | https://github.com/DeimosC2/DeimosC2 |
| MacC2 | python 3.8.6 w/aiohttp 3 | 2ad2ad0002ad2ad22c42d42d000000faabb8fd156aa8b4d8a37853e1063261 | https://github.com/cedowens/MacC2 |
| MacC2 | python 3.8.2 w/aiohttp 3 | 2ad2ad0002ad2ad00042d42d000000ad9bf51cc3f5a1e29eecb81d0c7b06eb | https://github.com/cedowens/MacC2 |
| MacShellSwift | python 3.8.6 socket | 2ad000000000000000000000000000eeebf944d0b023a00f510f06a29b4f46 | https://github.com/cedowens/MacShellSwift |
| MacShell | python 3.8.6 socket | 2ad000000000000000000000000000eeebf944d0b023a00f510f06a29b4f46 | https://github.com/cedowens/MacShellSwift |
| Sliver | go 1.15.2 linux/amd64 | 2ad2ad0002ad2ad00041d2ad2ad41da5207249a18099be84ef3c8811adc883 | https://github.com/BishopFox/sliver |
| EvilGinx2 | go 1.10.4 linux/amd64 | 20d14d20d21d20d20c20d14d20d20daddf8a68a1444c74b6dbe09910a511e6 | https://github.com/kgretzky/evilginx2 |
| Shad0w | python 3.8 flask | 2ad2ad0002ad2ad00042d42d000000ad9bf51cc3f5a1e29eecb81d0c7b06eb | https://github.com/bats3c/shad0w |
| Get2 | N/A | 07d19d12d21d21d07c07d19d07d21da5a8ab90bcc6bf8bbc6fbec4bcaa8219 | |
| GRAT2 C2 | python3 http.server | 2ad2ad0002ad2ad00042d42d000000ad9bf51cc3f5a1e29eecb81d0c7b06eb | https://github.com/r3nhat/GRAT2 |
| Covenant | ASP.net core | 21d14d00000000021c21d14d21d21d1ee8ae98bf3ef941e91529a93ac62b8b | https://github.com/cobbr/Covenant |
| SILENTRINITY | ironpython | 2ad2ad0002ad2ad00042d42d000000ad9bf51cc3f5a1e29eecb81d0c7b06eb | https://github.com/byt3bl33d3r/SILENTTRINITY |
| PoshC2 | python3 http.server | 2ad2ad0002ad2ad22c42d42d000000faabb8fd156aa8b4d8a37853e1063261 | https://github.com/nettitude/PoshC2