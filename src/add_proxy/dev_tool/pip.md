# pip

给pip临时，单次，加代理，可以用`--proxy proxy_address`

## Mac中给pip加代理 提高下载速度

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
