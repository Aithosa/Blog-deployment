# Ubuntu 防火墙设置

linux 2.4 内核以后提供了一个非常优秀的防火墙工具：`netfilter/iptables`，其免费且功能强大，可以对流入、流出的信息进行细化控制，可以实现防火墙、NAT（网络地址翻译）和数据包的分割等功能。netfilter 工作在内核内部，而 iptables 则是让用户定义规则集的表结构。

但是 iptables 的规则稍微有些“复杂”，因此 ubuntu 提供了 ufw 这个设定工具，以简化 iptables 的某些设定，其后台仍然是 iptables。ufw 即 uncomplicated firewall 的简称，一些复杂的设定还是要去 iptables。

ufw 相关的文件和文件夹有：

**`/etc /ufw/`**：里面是一些 ufw 的环境设定文件，如 `before.rules`、`after.rules`、`sysctl.conf`、`ufw.conf`，及 for ip6 的 `before6.rule` 及 `after6.rules`。这些文件一般按照默认的设置进行就可以。

开启 ufw 之后，`/etc/ufw/sysctl.conf` 会覆盖默认的 `/etc/sysctl.conf` 文件，若原来的 `/etc/sysctl.conf` 做了修改，启动 ufw 后，如 `/etc/ufw/sysctl.conf` 中有新赋值，则会覆盖 `/etc/sysctl.conf` 的值，否则还以 `/etc/sysctl.conf` 为准。当然你可以通过修改`/etc/default/ufw`中的“IPT_SYSCTL=”条目来设置使用哪个 `sysctrl.conf`。

**`/var/lib/ufw/user.rules`**: 这个文件中是我们设置的一些防火墙规则，打开大概就能看明白，有时我们可以直接修改这个文件，不用使用命令来设定。修改后记得`ufw reload`重启 ufw 使得新规则生效。

## ufw

ufw 是 Ubuntu 自带的防火墙。由于 Linux 原始的防火墙工具 iptables 过于繁琐，所以 ubuntu 默认提供了一个基于 iptable 之上的防火墙工具 ufw。

### 安装及查看

安装ufw

    $ sudo apt-get install ufw
    $ sudo apt install ufw    # 安装ufw

查看防火墙版本

    $ sudo ufw version    # 查看防火墙版本

显示防火墙和端口的侦听状态，参见 `/var/lib/ufw/maps` 。括号中的数字将不会被显示出来。

    $ sudo ufw status    # 可检查防火墙的状态

### 开启/禁用设置

    $ sudo ufw enable|disable    # 开启/关闭防火墙 (默认设置是’disable’)

    $ sudo ufw enable    # 开启防火墙

    $ sudo ufw default allow|deny    # 设置默认策略 (比如 “mostly open” vs “mostly closed”)
                                     # 可在“status” 中查看服务列表

    $ sudo ufw default deny    # 启动默认防御（阻止外部联接，放行对外联接）

    $ sudo ufw logging on|off    # 转换日志状态

    $ sudo ufw reload    # 重启ufw

### 规则添加

可以用"协议：端口"的方式指定一个存在于 `/etc/services` 中的服务名称，也可以通过包的 `meta-data` 。
<br>'allow' 参数将把条目加入 `/etc/ufw/maps` ，而 'deny' 则相反。

    sudo ufw allow|deny [service]

打开或关闭某个端口，例如：

    $ sudo ufw allow smtp    # 允许所有的外部IP访问本机的25/tcp (smtp)端口
                             # UFW也可以检查 `/etc/services`文件，明白服务的名字及对应的端口和协议

    $ sudo ufw allow 22/tcp    # 允许所有的外部IP访问本机的22/tcp (ssh)端口

    $ sudo ufw allow 53    # 允许外部访问53端口(tcp/udp)

    $ sudo ufw allow 1723/tcp    # 设置允许访问 pptp

    $ sudo ufw allow from 192.168.1.100    # 允许此IP访问所有的本机端口

    $ sudo ufw allow proto udp 192.168.0.1 port 53 to 192.168.0.2 port 53

UFW 同时支持出入口过滤。用户可以使用 `in` 或 `out` 来指定向内还是向外。如果未指定，默认是:

    $ sudo inufw allow in http    # 许可访问本机http端口，默认

    $ sudo ufw reject out smtp    # 禁止访问外部smtp端口，不告知“被防火墙阻止”

    $ sudo ufw deny out to 192.168.1.1    # 禁止本机192.168.1.1对外访问，告知“被防火墙阻止”

    $ sudo ufw deny smtp    # 禁止外部访问smtp服务

    $ sudo ufw delete allow smtp
    $ sudo ufw delete deny 80/tcp
    $ sudo ufw delete allow from 192.168.1.100    # 删除上面建立的某条规则

### 使用建议

一般用户只需如下设置：

    $ sudo apt-get install ufw
    $ sudo ufw enable
    $ sudo ufw default deny

以上三条命令已经足够安全了，如果你需要开放某些服务，再使用`sudo ufw allow`开启。

### Web blog服务器配置

    $ sudo ufw enable
    $ sudo ufw default deny
    $ sudo ufw allow 22/tcp    # 设置允许访问 SSH
    $ sudo ufw allow 80/tcp    # 设置允许访问 http
    $ sudo ufw allow 443/tcp    # 设置允许访问 https

### 参考

- [如何启动、关闭和设置 ubuntu 防火墙](https://www.cnblogs.com/yuxuan007/p/8043419.html)
- [Ubuntu16.04 自带防火墙 ufw 配置和用法](https://blog.csdn.net/u014389734/article/details/81814247)
