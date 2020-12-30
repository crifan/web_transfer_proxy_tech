# SecureCRT

## 给SecureCRT的ssh加代理

**背景**：用SecureCRT的ssh登录操作远程的CentOS的VPS服务器

但是速度太慢了，现象是：操作太卡了，输入命令反应太慢了。

希望能给SecureCRT的ssh加上（科学上网的）代理，提高访问速度。

**实现方式**： 通过Firewall实现ssh的proxy代理

**具体步骤**：

此处需要去给`全局配置`=`Global Options`

![securecrt_global_options](../../../assets/img/securecrt_global_options.png)

加上配置。

点击Add

![securecrt_firewall_add](../../../assets/img/securecrt_firewall_add.png)

弹出对话框：`FirewallPropertiesDialog`

![securecrt_firewallpropertiesdialog](../../../assets/img/securecrt_firewallpropertiesdialog.png)

点击`Type`的`Generic/Telnet Proxy`，出现各种选项，此处选择`SOCKS5 version 5(no authentification)`：

![securecrt_proxy_type_socks5_no_auth](../../../assets/img/securecrt_proxy_type_socks5_no_auth.png)

表示是用的`SOCK5`的协议，且无用户名密码的验证。

此处用前面的[从客户端获取代理配置 · 网络中转站：代理技术](http://book.crifan.com/books/web_transfer_proxy_tech/website/got_proxy/science_proxy/client_config.html)获取到了代理配置，比如：

```bash
export HTTP_PROXY=http://127.0.0.1:58591; export HTTPS_PROXY=http://127.0.0.1:58591; export ALL_PROXY=socks5://127.0.0.1:51837
```

此处去填上对应代理配置信息：

* `Name`:：随便起个名字
  * 比如：`local_socks5`
* `Type`：`SOCKS version 5 (no authentication)`
* `Parameters`
  * `Hostname or IP`：`127.0.0.1`
  * `Port`：`51837`

![securecrt_fill_proxy_config](../../../assets/img/securecrt_fill_proxy_config.png)

再点击`OK`，即可返回代理配置列表：

![securecrt_added_proxy_list](../../../assets/img/securecrt_added_proxy_list.png)

再编辑当前的`Session Options`

![securecrt_current_session_options](../../../assets/img/securecrt_current_session_options.png)

此处Firewall是灰色，无法修改

![securecrt_firewall_gray_no_edit](../../../assets/img/securecrt_firewall_gray_no_edit.png)

所以需要先去断开连接，再去修改

![securecrt_session_diconnect](../../../assets/img/securecrt_session_diconnect.png)

断开后，就可以去选择刚新建的Firewall：`local_socks5`

![securecrt_firewall_select](../../../assets/img/securecrt_firewall_select.png)

即可成功设置防火墙=此处的代理：

![securecrt_firewall_proxy](../../../assets/img/securecrt_firewall_proxy.png)

然后再去输入命令就会很顺畅，不会卡顿了：

![securecrt_input_cmd_smooth](../../../assets/img/securecrt_input_cmd_smooth.png)
