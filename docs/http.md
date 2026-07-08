# http

All HTTP calls are asynchronous.

## options

```lua
headers: table<string, string>
data: string | nil
contentType: string | nil
asTable: boolean
saveToFile: string | nil
```

`headers` are sent as request headers. `data` and `contentType` are used by `http.post`. When `asTable` is `true`, table `data` is converted into URL-encoded form data. `saveToFile` writes the response body to disk and passes an empty string to the callback.

## get

```lua
http.get(url: string, options: table, callback: function)
```

Performs a GET request. The callback receives `status_code` and `data`. `status_code` is `false` on request errors.

```lua
http.get("https://example.com", { headers = { ["x-test"] = "neverfair" } }, function(status, data)
    if status == 200 then
        print(data)
    end
end)
```

## post

```lua
http.post(url: string, options: table, callback: function)
```

Performs a POST request. `contentType` defaults to `application/x-www-form-urlencoded`.

```lua
http.post("https://example.com", { headers = { ["x-test"] = "neverfair" }, contentType = "application/json", data = "{\"value\":123}" }, function(status, data)
    if status == 200 then
        menu.notify("post ok")
    end
end)
```

## example

```lua
http.get("https://example.com", {}, function(status, data)
    if status == false then
        menu.notify("http failed", color_t(1, 0.2, 0.2, 1))
        return
    end

    menu.notify("http status " .. tostring(status))
end)
```
