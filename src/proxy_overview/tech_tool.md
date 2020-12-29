# 代理相关技术和工具

对于不同用途的代理，对应的所用技术和工具是：

* 爬虫
  * 涉及：
    * 服务
      * 免费或收费的代理
        * 免费
          * 网上找免费可用代理
        * 收费
          * 自己从某代理服务（卖代理的网站）中购买对应代理（服务）
            * 比如
              * 阿布云代理
              * 多贝云代理
* (app)抓包
  * 涉及：
    * 工具
      * `Charles`
        * [app抓包利器：Charles](https://book.crifan.com/books/app_capture_package_tool_charles/website)
      * mitmproxy
        * [抓包代理利器：mitmproxy](https://book.crifan.com/books/crawler_proxy_tool_mimproxy/website)
    * wireshark
* 科学上网(翻墙)
  * 涉及
    * 技术
      * Shadowsocks
      * V2Ray
      * Trojan
    * 工具
      * 对应客户端
        * ShadowsocksX-NG
        * V2rayU
        * Trojan-QT5

## 代理协议种类

不论是哪种代理，都涉及到代理的协议种类：

* 常见代理协议种类
  * `http`
  * `https`
  * `socks`
    * 协议
      * `SOCKS4`
      * `SOCKS5`
    * `SOCKS`代理
      * 只是单纯传递数据包，不关心具体协议和用法，所以速度快很多
      * 端口一般为：`1080`
