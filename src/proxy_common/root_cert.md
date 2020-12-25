# 安装根证书

* 安装根证书
  * 安装代理证书
    * 给Charles安装根证书
    * 给mitmproxy安装根证书
  * 通用逻辑
    * pc端
      * 开启代理
    * 移动端
      * 给WiFi加上代理
      * 用浏览器访问网址下载代理证书
        * 访问网址
          * Charles地址
            * http://chls.pro/ssl
          * mitmproxy地址
            * http://mitm.it
              * 如果没给WiFi加代理则会提示
                * `if you can see this, traffic is not passing through mitmproxy`
        * 证书文件
          * 正常时
            * Charles: `charles-proxy-ssl-proxying-certificate.pem`
              * 有时是: `getssl.crt`
            * mitmproxy: `mitmproxy-ca-cert.pem`
          * 异常时：无法下载
            * Charles: `downloadfile.crt`
            * mitmproxy: `perm.crt`
