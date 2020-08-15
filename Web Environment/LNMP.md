# LNMP 环境配置

之前也手动配置过 LNMP 环境，虽然能用，但是不知道中间有没有问题，所以还是使用一键安装包比较放心。

地址：<https://lnmp.org/install.html>

## 系统需求

- CentOS/RHEL/Fedora/Debian/Ubuntu/Raspbian/Deepin/Aliyun/Amazon/Mint Linux 发行版
- 需要 5GB 以上硬盘剩余空间，MySQL 5.7, MariaDB 10 至少 9GB 剩余空间
- 需要 128MB 以上内存(128MB 小内存 VPS, Xen 需有 SWAP, OpenVZ 至少要有 128MB 以上的 vSWAP 或突发内存)，注意小内存请勿使用 64 位系统！
- **安装 MySQL 5.6 或 5.7 及 MariaDB 10 必须 1G 以上内存，更高版本至少要 2G 内存!。**
- **安装 PHP 7 及以上版本必须 1G 以上内存!。**
- VPS 或服务器必须设置好可用的`yum`或`apt-get`源并确保能正常工作，离线安装需要增加 `CheckMirror=n` 参数！
- Linux 下区分大小写，输入命令时请注意！
- 如有通过`yum`或`apt-get`安装的 MySQL/MariaDB 请自行备份数据等相关文件！
- CentOS 5, Debian 6 及之前版本其官网已经结束支持无法使用！
- Ubuntu 18+, Debian 9+, Mint 19+, Deepin 15.7+ 及所有新的 Linux 发行版只能使用 1.7 进行安装！
- PHP 7.1.\* 以下版本不支持 Ubuntu 19+、Debian 10 等等非常新的 Linux 发行版！
- 阿里云 Ubuntu 14.04 系统模版有问题不要用！！！
- PHP 7.4 升级或安装必须 CentOS 7+, Debian 8+, Ubuntu 16.04+ 且必须使用 1.7！！！
- MySQL 8.0 升级或安装必须 CentOS 8+, Debian 9+, Ubuntu 16.04+ 且必须使用 1.7！！！

> Ubuntu 20.04 只能使用 1.7 版本安装包，且使用 PHP 7.1 及以上脚本，因此内存必须 1G 以上。

## 安装步骤

### 1、使用 putty 或类似的 SSH 工具登陆 VPS 或服务器

登陆后运行：`screen -S lnmp`
<br>如果提示`screen: command not found` 命令不存在可以执行：`yum install screen` 或 `apt-get install screen`安装，详细内容参考[screen 教程](https://www.vpser.net/manage/run-screen-lnmp.html)。

> Ubuntu 服务器刚设置好可能只有 root 用户及密码，若不是服务器可以执行`sudo passwd root`设置 root 用户的密码。

### 2、下载并安装 LNMP 一键安装包

您可以选择使用下载版(推荐美国及海外 VPS 或空间较小用户使用)或者完整版(推荐国内 VPS 使用，国内用户可用在[下载](https://lnmp.org/download.html)中找国内下载地址替换)，两者没什么区别，只是完整版把一些需要的源码文件预先放到安装包里。

#### 安装 LNMP 稳定版

如需无人值守安装，请使用[无人值守命令生成工具](https://lnmp.org/auto.html)，或查看[无人值守说明教程](https://lnmp.org/faq/v1-5-auto-install.html)

	$ wget http://soft.vpser.net/lnmp/lnmp1.7.tar.gz -cO lnmp1.7.tar.gz && tar zxf lnmp1.7.tar.gz && cd lnmp1.7 && ./install.sh lnmp

如需要安装 LNMPA 或 LAMP，将`./install.sh`后面的参数 lnmp 替换为 lnmpa 或 lamp 即可。如需更改网站和数据库目录、自定义 Nginx 参数、PHP 参数模块、开启 lua 等需在运行`./install.sh` 命令前修改安装包目录下的 lnmp.conf 文件，详细可以查看 lnmp.conf 文件参数说明。

> 如提示 wget: command not found ，使用`yum install wget` 或 `apt-get install wget` 命令安装。

如下载速度慢或无法下载请更换其他下载节点，请查看[LNMP 下载节点具体替换方法](https://lnmp.org/faq/lnmp-download-source.html)。

运行上述 LNMP 安装命令后，会出现如下提示：

```
+------------------------------------------------------------------------+
|          LNMP V1.7 for Ubuntu Linux Server, Written by Licess          |
+------------------------------------------------------------------------+
|        A tool to auto-compile & install LNMP/LNMPA/LAMP on Linux       |
+------------------------------------------------------------------------+
|           For more information please visit https://lnmp.org           |
+------------------------------------------------------------------------+
You have 11 options for your DataBase install.
1: Install MySQL 5.1.73
2: Install MySQL 5.5.62 (Default)
3: Install MySQL 5.6.48
4: Install MySQL 5.7.30
5: Install MySQL 8.0.20
6: Install MariaDB 5.5.68
7: Install MariaDB 10.1.45
8: Install MariaDB 10.2.32
9: Install MariaDB 10.3.23
10: Install MariaDB 10.4.13
0: DO NOT Install MySQL/MariaDB
Enter your choice (1, 2, 3, 4, 5, 6, 7, 8, 9, 10 or 0):
```

MySQL 安装默认的就行：2

密码：`#yU,hM-GrG9_Pj`, 服务器密码请设置强密码。

```
Please setup root password of MySQL.
Please enter: #yU,hM-GrG9_Pj
MySQL root password: #yU,hM-GrG9_Pj
```

设置 MySQL 的 root 密码（为了安全不输入直接回车将会设置为 lnmp.org#随机数字）如果输入有错误需要删除时，可以按住 Ctrl 再按 Backspace 键进行删除(个别情况下是只需要 Backspace 键)。输入后回车进入下一步

```
Do you want to enable or disable the InnoDB Storage Engine?
Default enable,Enter your choice [Y/n]: y
You will enable the InnoDB Storage Engine
```

询问是否需要启用 MySQL InnoDB，InnoDB 引擎默认为开启，一般建议开启，直接回车或输入 y ，如果确定确实不需要该引擎可以输入 n，(MySQL 5.7+版本无法关闭 InnoDB),输入完成，回车进入下一步。

```
You have 9 options for your PHP install.
1: Install PHP 5.2.17
2: Install PHP 5.3.29
3: Install PHP 5.4.45
4: Install PHP 5.5.38
5: Install PHP 5.6.40 (Default)
6: Install PHP 7.0.33
7: Install PHP 7.1.33
8: Install PHP 7.2.32
9: Install PHP 7.3.20
10: Install PHP 7.4.8
Enter your choice (1, 2, 3, 4, 5, 6, 7, 8, 9, 10):
```

由于是 Ubuntu 20.04, 选择 7-10, 这里选择 7 即可

```
You have 3 options for your Memory Allocator install.
1: Don't install Memory Allocator. (Default)
2: Install Jemalloc
3: Install TCMalloc
Enter your choice (1, 2 or 3):
```

可以选择不安装、Jemalloc 或 TCmalloc，输入对应序号回车，直接回车为默认为不安装。

如果是 LNMPA 或 LAMP 的话还会提示设置邮箱和选择 Apache“Please enter Administrator Email Address:”，需要设置管理员邮箱，该邮箱会在报错时显示在错误页面上。

再选择 Apache 版本

按提示输入对应版本前面的数字序号，回车。

提示"Press any key to install...or Press Ctrl+c to cancel"后，按回车键确认开始安装。
LNMP 脚本就会自动安装编译 Nginx、MySQL、PHP、phpMyAdmin 等软件及相关的组件。

安装时间可能会几十分钟到几个小时不等，主要是机器的配置网速等原因会造成影响。

> 用的服务器还好，如果是本地虚拟机最好改一下源。

### 3、安装完成

如果显示 Nginx: OK，MySQL: OK，PHP: OK

并且 Nginx、MySQL、PHP 都是 running，80 和 3306 端口都存在，并提示安装使用的时间及 Install lnmp V1.6 completed! enjoy it.的话，说明已经安装成功。

```
============================== Check install ==============================
Checking ...
Nginx: OK
MySQL: OK
PHP: OK
PHP-FPM: OK
Clean Web Server src directory...
+------------------------------------------------------------------------+
|          LNMP V1.7 for Ubuntu Linux Server, Written by Licess          |
+------------------------------------------------------------------------+
|           For more information please visit https://lnmp.org           |
+------------------------------------------------------------------------+
|    lnmp status manage: lnmp {start|stop|reload|restart|kill|status}    |
+------------------------------------------------------------------------+
|  phpMyAdmin: http://IP/phpmyadmin/                                     |
|  phpinfo: http://IP/phpinfo.php                                        |
|  Prober:  http://IP/p.php                                              |
+------------------------------------------------------------------------+
|  Add VirtualHost: lnmp vhost add                                       |
+------------------------------------------------------------------------+
|  Default directory: /home/wwwroot/default                              |
+------------------------------------------------------------------------+
|  MySQL/MariaDB root password: #yU,hM-GrG9_Pj                          |
+------------------------------------------------------------------------+
+-------------------------------------------+
|    Manager for LNMP, Written by Licess    |
+-------------------------------------------+
|              https://lnmp.org             |
+-------------------------------------------+
nginx (pid 94183) is running...
php-fpm is runing!
● mysql.service - MySQL Community Server
     Loaded: loaded (/etc/systemd/system/mysql.service; enabled; vendor preset: enabled)
     Active: active (running) since Thu 2020-08-13 08:11:34 CST; 1s ago
   Main PID: 336940 (mysqld_safe)
      Tasks: 17 (limit: 4587)
     Memory: 58.3M
     CGroup: /system.slice/mysql.service
             ├─336940 /bin/sh /usr/local/mysql/bin/mysqld_safe --datadir=/usr/local/mysql/var --pid-file=/usr/local/mysql/var/riddle.pid
             └─337434 /usr/local/mysql/bin/mysqld --basedir=/usr/local/mysql --datadir=/usr/local/mysql/var --plugin-dir=/usr/local/mysql/lib/plugin --user=mysql --log-error=riddle.err --open-files-limit=65535 --pid-file=/usr/local/mysql/var/riddle.pid --socket=/tmp/mysql.sock --port=3306

Aug 13 08:11:32 riddle systemd[1]: Starting MySQL Community Server...
Aug 13 08:11:32 riddle mysql[336926]: Starting MySQL
Aug 13 08:11:34 riddle mysql[336926]: .. *
Aug 13 08:11:34 riddle systemd[1]: Started MySQL Community Server.
State    Recv-Q   Send-Q     Local Address:Port     Peer Address:Port  Process
LISTEN   0        511              0.0.0.0:80            0.0.0.0:*
LISTEN   0        511              0.0.0.0:80            0.0.0.0:*
LISTEN   0        4096       127.0.0.53%lo:53            0.0.0.0:*
LISTEN   0        128              0.0.0.0:22            0.0.0.0:*
LISTEN   0        50               0.0.0.0:3306          0.0.0.0:*
LISTEN   0        128                 [::]:22               [::]:*
Install lnmp takes 19 minutes.
Install lnmp V1.7 completed! enjoy it.
```

某些系统可能会一直卡在 Install lnmp V1.5 completed! enjoy it.不自动退出，可以按`Ctrl+c`退出。

安装完成接下来开始使用就可以了，按添加虚拟主机教程，添加虚拟主机后可以使用 sftp 或 ftp 服务器上传网站代码，将域名解析到 VPS 或服务器的 IP 上，解析生效即可使用。

### 4、安装失败

![安装失败](https://lnmp.org/images/1.5/lnmp1.5-install-failed.png)

如果出现类似上图的提示，有一个或几个没安装成功表明安装失败！！需要用 winscp 或其他类似工具，将/root 目录下面的 lnmp-install.log 下载下来，到 LNMP 支持论坛发帖注明你的系统发行版名称及版本号、32 位还是 64 位等信息，并将 lnmp-install.log 压缩以附件形式上传到论坛，我们会通过日志查找错误，并给予相应的解决方法。

默认 LNMP 是不安装 FTP 服务器的，如需要 FTP 服务器：<https://lnmp.org/faq/ftpserver.html>

### 5、添加、删除虚拟主机及伪静态管理

<https://lnmp.org/faq/lnmp-vhost-add-howto.html>

### 6、eAccelerator、xcache、memcached、imageMagick、ionCube、redis、opcache 的安装

<https://lnmp.org/faq/addons.html>

### 7、LNMP 相关软件目录及文件位置

<https://lnmp.org/faq/lnmp-software-list.html>

### 8、LNMP 状态管理命令

<https://lnmp.org/faq/lnmp-status-manager.html>

### 9、仅安装数据库、Nginx

lnmp 1.5 开始支持只安装 MySQL/MariaDB 数据库或 Nginx
增加单独 nginx 安装，安装包目录下运行：`./install.sh nginx` 进行安装；
增加单独数据库安装，安装包目录下运行：`./install.sh db` 进行安装；

### 10、lnmp 一键安装包支持完全离线模式进行安装

CentOS 系统下离线安装教程：<https://www.vpser.net/manage/centos-iso-local-yum-repository.html>
Debian/Ubuntu 发行版下类似。
