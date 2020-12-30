# git

git 添加 代理 加速

* 简述：
    ```bash
    git config --global http.proxy socks5://127.0.0.1:51837
    git config --global --unset http.proxy
    ```
* 详解：
  * git中没有可以设置，当前这次的，临时的，只有一次的代理
  * 只能间接的实现，此处单独针对于GitHub的
    * 全局的设置代理
      * `git config --global http.https://github.com.proxy socks5://127.0.0.1:1086`
      * `git config --global http.https://github.com.proxy socks5://127.0.0.1:51837`
    * 用`git clone`下载时，就可以用上代理实现下载加速了
      * `git clone https://github.com/appium/WebDriverAgent.git`
    * 用完再去取消代理
      * `git config --global --unset http.https://github.com.proxy`
* 说明
  * 代理协议
    * 可以把上述的`socks5://127.0.0.1:1086`换成其他协议的代理，比如`http`的`http://127.0.0.1:1086`
  * 代理端口
    * 上述端口是：1086
      * 如果你的端口不是1086，千万记得要更换成自己的代理的端口
  * 查看当前git的代理配置
    * 随时可以用
      * `cat ~/.gitconfig`
    * 查看当前全局的设置，是否正确
    * 结果有几种情况：
      * 已设置了代理
        ```bash
        [http "https://github.com"]
          proxy = socks5://127.0.0.1:1086
        ```
      * 已取消了代理
        * 看不到http部分的proxy字段

## 给git加代理使用心得

### error: RPC failed; curl 35 LibreSSL SSL_connect

如果git下载报错

`error: RPC failed; curl 35 LibreSSL SSL_connect`

可以多试几次，或许就好了。

比如，之前遇到过几次，git下载报错了：

```bash
➜  temp git clone https://github.com/fcamblor/oh-my-zsh-agnoster-fcamblor.git
Cloning into 'oh-my-zsh-agnoster-fcamblor'...
error: RPC failed; curl 35 LibreSSL SSL_connect: SSL_ERROR_SYSCALL in connection to github.com:443
fatal: the remote end hung up unexpectedly
➜  temp git clone https://github.com/fcamblor/oh-my-zsh-agnoster-fcamblor.git
Cloning into 'oh-my-zsh-agnoster-fcamblor'...
remote: Enumerating objects: 136, done.
remote: Total 136 (delta 0), reused 0 (delta 0), pack-reused 136
Receiving objects: 100% (136/136), 1.14 MiB | 741.00 KiB/s, done.
Resolving deltas: 100% (59/59), done.
```

此时并没有改动代理服务器节点，而是多试了一次（或多次），就又好了。

### 只对某些url用代理，不对另外一些url用代理

比如：只对`github`用代理，而对`gitee`不用代理

修改配置为：

```bash
[http]
    proxy = socks5://127.0.0.1:1086
[http "https://gitee.com/"]
    proxy =
```
