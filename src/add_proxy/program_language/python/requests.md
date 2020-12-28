# requests

## python的网络库requests中加proxy代理

前提：确保自己的代理正常。比如此处的`V2RayU`中的代理：

![v2rayu_proxy](../../../assets/img/v2rayu_proxy.png)

代码：

此处给（调用WordPress的REST的api时的）网络请求加上代理：

```python
cfgProxies = {
    "http"  : "http://127.0.0.1:1087",
    "https" : "http://127.0.0.1:1087",
}

resp = requests.post(
    createPostUrl,
    proxies=cfgProxies,
    headers=curHeaders,
    json=postDict,
)
```

即可。

## PySpider中使用代理

爬虫框架[PySpider](http://book.crifan.com/books/python_spider_pyspider/website)内部用的是`requests`，其设置代理的方式，也就是和requests一样了。

PySpider中设置了全局的代理：

```python
### dobel 多贝云 IP代理
#http代理接入服务器地址端口
ProxyHost = "http-proxy-t3.dobel.cn"
ProxyPort = "9180"

#账号密码
ProxyUser = "YourUserName"
ProxyPass = "YourPassword"

ProxyUri = "http://%(user)s:%(pass)s@%(host)s:%(port)s" % {
        "host" : ProxyHost,
        "port" : ProxyPort,
        "user" : ProxyUser,
        "pass" : ProxyPass,
}

class Handler(BaseHandler):
    crawl_config = {
        "proxy": ProxyUri,
        ...
    }
```

之后的self.crawl正常调用url，即可用上此处的代理了。

其中ProxyUri是这种：

`http://YourUserName:YourPassword@http-proxy-t3.dobel.cn:9180`
