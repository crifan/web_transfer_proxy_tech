# 移动端

给移动端设置代理之前，往往要：

* 主机
  * 确保已开代理服务
    * 比如
      * Mac中运行了[mitmdump](https://book.crifan.com/books/crawler_proxy_tool_mimproxy/website)代理服务
      * Mac中打开了[Charles](https://book.crifan.com/books/app_capture_package_tool_charles/website)软件
  * 知道当前主机的IP地址

## 查看当前主机的IP

在给移动端（手机等）设置代理之前，往往对应的代理IP地址都是PC端主机地址。

所以需要去查看当前的主机的IP地址。

Mac中查看自己的IP地址的方式可以用命令行：

```bash
crifanli@crifanlideMac  ~  ifconfig | grep 192.168
    inet 192.168.17.128 netmask 0xffffff00 broadcast 192.168.17.255
```

其中可以看出，Mac中的WiFi网络的IP是：

`192.168.17.128`
