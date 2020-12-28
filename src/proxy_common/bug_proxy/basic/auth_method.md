# 认证方式

IP代理中的认证方式，常见的有几种。

此处介绍最简单最基本的：

## HTTP基本认证

另外，也从：

* [隧道代理接入文档 | 蜻蜓代理 - 企业级高质量代理ip平台](https://proxy.horocn.com/news/wQqd.html)
    > 目前，我们使用的是 HTTP基本认证，在发送请求中，添加`Proxy-Authorization`头部，值为：`Basic b64encode("username:password")`。

得知了，此处一般IP代理提供商的认证方式，都是用的是：

`Http Basic Authentication`=`Http基本认证`

-》最通用，也相对最简单的方式

-》所以其他很多http方面的库，比如Python的requests，也才会（内置就）支持

所以示例代码中：

https://github.com/dobelgit/dobelcloud/blob/master/Python/PythonRequestsDemo.py

```python
#! -*- encoding:utf-8 -*-

import requests

#目标网址
targetUrl = "https://www.taobao.com/help/getip.php"

#http代理接入服务器地址端口
proxyHost = "域名"
proxyPort = "端口"

#账号密码
proxyUser = "账号"
proxyPass = "密码"

proxyMeta = "http://%(user)s:%(pass)s@%(host)s:%(port)s" % {
        "host" : proxyHost,
        "port" : proxyPort,
        "user" : proxyUser,
        "pass" : proxyPass,
}

proxies = {
        "http"  : proxyMeta,
        "https" : proxyMeta,
}

result = requests.get(targetUrl, proxies=proxies)

print result.status_code
print result.text
```

只需要传递参数，无需手动自己算base64编码等过程了

后续发现其他IP代理服务的认证也是这个种方式：

[蘑菇代理 - 购买API代理](http://www.moguproxy.com/http)

其他的也是：

[动态版HTTP隧道接入指南 | 阿布云 - 为大数据赋能](https://www.abuyun.com/http-proxy/dyn-manual.html)

-》示例代码都是一样的：

[abuyun/proxy-demo: abuyun cloud proxy demo](https://github.com/abuyun/proxy-demo)

[HTTP隧道（动态版）Python 接入指南| 阿布云 - 为大数据赋能](https://www.abuyun.com/http-proxy/dyn-manual-python.html)

```python
#! -*- encoding:utf-8 -*-

import requests
# 要访问的目标页面
targetUrl = "http://test.abuyun.com"
#targetUrl = "http://proxy.abuyun.com/switch-ip"
#targetUrl = "http://proxy.abuyun.com/current-ip"
# 代理服务器
proxyHost = "http-dyn.abuyun.com"
proxyPort = "9020"
# 代理隧道验证信息
proxyUser = "H01234567890123D"
proxyPass = "0123456789012345"
proxyMeta = "http://%(user)s:%(pass)s@%(host)s:%(port)s" % {
    "host" : proxyHost,
    "port" : proxyPort,
    "user" : proxyUser,
    "pass" : proxyPass,
}
proxies = {
    "http"  : proxyMeta,
    "https" : proxyMeta,
}
resp = requests.get(targetUrl, proxies=proxies)
print resp.status_code
print resp.text
```
