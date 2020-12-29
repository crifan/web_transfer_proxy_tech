# rsync

给rsync加代理加速，即可以通过给rsync加代理，实现加快文件同步上传的速度。

具体方式是：

* 加代理之前
  * sshpass -f /Users/crifan/dev/dev_root/gitbook/gitbook_src_root/common/config/deploy/deploy_server_password.txt rsync -avzh --progress --stats --delete --force /Users/crifan/dev/dev_root/gitbook/gitbook_src_root/generated/books/android_app_security_crack/release/android_app_security_crack root@149.28.136.189:/data/wwwroot/book.crifan.com/books
* 加代理之后
  * sshpass -f /Users/crifan/dev/dev_root/gitbook/gitbook_src_root/common/config/deploy/deploy_server_password.txt rsync -avzh --progress --stats --delete --force **-e "ssh -o 'ProxyCommand nc -X 5 -x 127.0.0.1:51837 %h %p' -o ServerAliveInterval=30 -o ServerAliveCountMax=5"** /Users/crifan/dev/dev_root/gitbook/gitbook_src_root/generated/books/android_app_security_crack/release/android_app_security_crack root@149.28.136.189:/data/wwwroot/book.crifan.com/books

其中参数含义解释：

* rsync
  * `-e, --rsh=COMMAND`
    * specify the remote shell to use
      * `ssh -o 'ProxyCommand nc -X 5 -x 127.0.0.1:51837 %h %p' -o ServerAliveInterval=30 -o ServerAliveCountMax=5`
* ssh
  * `-o option`
    * Can be used to give options in the format used in the configuration file. This is useful for specifying options for which there is no separate command-line flag. For full details of the options listed below, and their possible values
      * ProxyCommand
* `nc -X 5 -x 127.0.0.1:51837 %h %p`
  * 参数语法
    * `-X proxy_version`
      * Requests that nc should use the specified protocol when talking to the proxy server. Supported protocols are ''4'' (SOCKS v.4), ''5'' (SOCKS v.5) and ''connect'' (HTTPS proxy). If the protocol is not specified, SOCKS version 5 is used.
    * `-x proxy_address[:port]`
      * Requests that nc should connect to hostname using a proxy at proxy_address and port. If port is not specified, the well-known port for the proxy protocol is used (1080 for SOCKS, 3128 for HTTPS).
  * 参数含义
    * `-X 5`
      * SOCKS 5版协议
        * 此处用的是SOCKS5代理（不是http代理）
    * `-x 127.0.0.1:1080`
      * 代理地址和端口是：127.0.0.1:1080
    * `%h %p`
      * 应该是对应着：`[hostname] [port[s]]`
        * 分别表示：
          * `%host`：当前主机 host ?
          * `%p`：当前端口 port ?
* ssh_config 
  * 参数语法
    * `ServerAliveInterval`
      * Sets a timeout interval in seconds after which if no data has been received from the server, ssh(1) will send a message through the encrypted channel to request a response from the server. The default is 0, indicating that these messages will not be sent to the server.
    * `ServerAliveCountMax`
      * Sets the number of server alive messages (see below) which may be sent without ssh(1) receiving any messages back from the server. If this threshold is reached while server alive messages are being sent, ssh will disconnect from the server, terminating the session. It is important to note that the use of server alive messages is very different from TCPKeepAlive(below). The server alive messages are sent through the encrypted channel and therefore will not be spoofable. The TCP keepalive option enabled by TCPKeepAlive is spoofable. The server alive mechanism is valuable when the client or server depend on knowing when a connection has become unresponsive.
      * The default value is 3. If, for example, ServerAliveInterval (see below) is set to 15 and ServerAliveCountMax is left at the default, if the server becomes unresponsive, ssh will disconnect after approximately 45 seconds.
  * 参数含义
    * `ServerAliveInterval=30`
      * 每次最多30秒
    * `ServerAliveCountMax=5`
      * 最多5次
