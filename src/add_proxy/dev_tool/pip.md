# pip

如果发现pip下载很慢，可以考虑加代理，提高下载速度：

## 给pip加单次的临时的代理，以提高下载速度

给pip临时的、单次的加代理，可以用`--proxy proxy_address`

单次加代理：

```bash
pip --proxy http://127.0.0.1:1087 install pandas
```

用法举例：

```bash
pip --proxy http://127.0.0.1:1087 install requests pyyaml uiautomator2 selenium tldextract pymongo redis pandas numpy

pip --proxy http://127.0.0.1:1087 install --upgrade pandas==0.24.2

pip --proxy http://127.0.0.1:1087 install pocoui
```

## Mac/Windows中给pip添加全局代理，以提高下载速度

从Trojan客户端获取到代理命令后，去运行：

* Windows
    ```bash
    set HTTP_PROXY=http://127.0.0.1:1081
    set HTTPS_PROXY=http://127.0.0.1:1081
    set ALL_PROXY=socks5://127.0.0.1:1080
    ```
* Mac/Linux
    ```bash
    export HTTP_PROXY=http://127.0.0.1:58591
    export HTTPS_PROXY=http://127.0.0.1:58591
    export ALL_PROXY=socks5://127.0.0.1:51837
    ```

详见：[桌面端 · 网络中转站：代理技术](http://book.crifan.com/books/web_transfer_proxy_tech/website/add_proxy/pc/)
