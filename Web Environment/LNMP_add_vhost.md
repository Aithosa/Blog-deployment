# LNMP 添加虚拟主机

一般情况下每个虚拟主机就是一个网站，网站一般通过域名进行访问。

虚拟主机管理基本命令介绍：`lnmp vhost {add|list|del}`

## 添加网站(虚拟主机)

> 如果输入有错误需要删除时，可以按住`Ctrl`再按`Backspace`键进行删除。

执行：`lnmp vhost add` 出现如下界面：

```
+-------------------------------------------+
|    Manager for LNMP, Written by Licess    |
+-------------------------------------------+
|              https://lnmp.org             |
+-------------------------------------------+
Please enter domain(example: www.lnmp.org):
```

这里要输入要添加网站的域名，我们以添加 www.vpser.net 域名为例，如上图提示后输入域名 www.vpser.net 回车后提示

> 注：本地使用也可以直接输入 ip 地址，但是只是用 ip 地址无法通过 Let's Encrypt 添加 SSL

```
 Your domain: www.vpser.net
 Enter more domain name(example: lnmp.org *.lnmp.org):
```

这里询问是否添加更多域名，直接再输入要绑定的域名，这里我们将 vpser.net 也绑上，多个域名空格隔开，如不需要绑其他域名就直接回车。

> 注：带 www 和不带 www 的是不同的域名，如需带 www 和不带的 www 的域名都访问同一个网站需要同时都绑定

下面需要设置网站的目录

```
Please enter the directory for the domain: www.vpser.net
Default directory: /home/wwwroot/www.vpser.net:
```

网站目录不存在的话会创建目录。也可以输入已经存在的目录或要设置的目录（注意如要输入必须是**全路径**即以/开头的完整路径！）。不输入直接回车的话，采用默认目录：`/home/wwwroot/域名`

```
Virtual Host Directory: /home/wwwroot/www.vpser.net
Allow Rewrite rule? (y/n)
```

伪静态可以使 URL 更加简洁也利于 SEO，如程序支持并且需要设置伪静态的话，如启用输入 y ，不启用输入 n 回车(注意 LNMPA 或 LAMP 模式没有该选择项！)。

```
Please enter the rewrite of programme,
wordpress,discuzx,typecho,thinkphp,laravel,codeigniter,yii2 rewrite was exist.
(Default rewrite: other):
```

默认已经有了 discuz、discuzx、discuzx2(Discuz X 二级目录)、wordpress、wp2(WordPress 二级目录)、typecho、typecho2(Typecho 二级目录)、sablog、emlog、dabr、phpwind、、dedecms、drupal、ecshop、shopex 等常用的 Nginx 伪静态配置文件，可以直接输入名称进行使用，如果是二级目录则需要对应配置文件里的二级目录的名称。

```
You choose rewrite: typecho
Enable PHP Pathinfo? (y/n)
Enable pathinfo.
```

这一步是设置日志，如启用日志输入 y ，不启用输入 n 回车。

```
Allow access log? (y/n)
Enter access log filename(Default:www.vpser.net.log):
```

如果启用需要再输入要设置的日志的名称，默认日志目录为：`/home/wwwlogs/` 默认文件名为：`域名.log` 回车确认后，会询问是否添加数据库和数据库用户。

```
Create database and MySQL user with same name (y/n)
```

如果需要添加数据库输入 y ，不添加数据库输入 n 回车。

```
Enter current root password of Database (Password will not shown):
```

如果要添加，需要先验证 MySQL 的 root 密码(注：输入密码将不显示)
提示 Enter database name: 后输入要创建的数据库名称，要创建的数据库用户名会和数据库同名，回车确认。

提示 Please enter password for mysql user 数据库名: 后输入要设置的密码，回车确认。

```
Enter database name: typecho_test
Your will create a database and MySQL user with same name: typecho_test
Please enter password for mysql user typecho_test: typecho_test_user
Your password: typecho_test_user
```

接下来是 1.4 新增的添加 SSL 功能

```
Add SSL Certificate (y/n)
```

如果需要添加输入 y ，不添加输入 n 回车。
选择了添加 SSL 会提示

```
1: Use your own SSL Certificate and Key
2: Use Let's Encrypt to create SSL Certificate and Key
Enter 1 or 2:
```

有两个选项

1-选项为使用自己准备好的 SSL 证书和 key。

![自备SSL](https://lnmp.org/images/1.4/lnmp1.4-vhost-add-14.png)

> > 提示 Please enter full path to SSL Certificate file 后输入要 SSL 证书的完整路径和文件名，回车确认。
> > 提示 Please enter full path to SSL Certificate Key file: 后输入输入要 key 文件的完整路径和文件名，回车确认。
> > LAMP 下会提示 Please enter full path to SSL Chain file: 一般 Apache2.2 需要用到这个添加上证书链，2.4 前面证书是补全证书链的话不用。

2-选项为使用免费 SSL 证书提供商 Letsencrypt 的证书，自动生成 SSL 证书等信息。

```
It will be processed automatically.
```

提示 Press any key to start create virtul host... 后，回车确认便会开始创建虚拟主机。

添加成功会提示添加的域名、目录、伪静态、日志、数据库、FTP 等相关信息，如下：

```
================================================
Virtualhost infomation:
Your domain: www.vpser.net
Home Directory: /home/wwwroot/www.vpser.net
Rewrite: typecho
Enable log: yes
Database username: typecho_test
Database userpassword: typecho_test_user
Database Name: typecho_test
Create ftp account: no
Enable SSL: yes
  =>Let's Encrypt
================================================
```

完整的配置输出如下：

```
root@riddle:~# lnmp vhost add
+-------------------------------------------+
|    Manager for LNMP, Written by Licess    |
+-------------------------------------------+
|              https://lnmp.org             |
+-------------------------------------------+
Please enter domain(example: www.lnmp.org): www.vpser.net
 Your domain: www.vpser.net
Enter more domain name(example: lnmp.org *.lnmp.org):  vpser.net
 domain list: vpser.net
Please enter the directory for the domain: www.vpser.net
Default directory: /home/wwwroot/www.vpser.net:
Virtual Host Directory: /home/wwwroot/www.vpser.net
Allow Rewrite rule? (y/n) y
Please enter the rewrite of programme,
wordpress,discuzx,typecho,thinkphp,laravel,codeigniter,yii2 rewrite was exist.
(Default rewrite: other): typecho
You choose rewrite: typecho
Enable PHP Pathinfo? (y/n) y
Enable pathinfo.
Allow access log? (y/n) y
Enter access log filename(Default:www.vpser.net.log):
You access log filename: www.vpser.net.log
Create database and MySQL user with same name (y/n) y
Enter current root password of Database (Password will not shown):
OK, MySQL root password correct.
Enter database name: typecho_test
Your will create a database and MySQL user with same name: typecho_test
Please enter password for mysql user typecho_test: typecho_test_user
Your password: typecho_test_user
Add SSL Certificate (y/n) y
1: Use your own SSL Certificate and Key
2: Use Let's Encrypt to create SSL Certificate and Key
Enter 1 or 2: 2
It will be processed automatically.

Press any key to start create virtul host...
```

## 伪静态管理

LNMPA 或 LAMP 可以直接使用网站根目录下放`.htaccess`来设置伪静态规则(具体规则可以去程序官网网站找 google 百度)，但是在 LNMP 下，需要使用 Nginx 伪静态规则。

伪静态可以随时添加或删除，如果添加完虚拟主机后忘记或没有添加伪静态，可以通过修改配置文件来添加伪静态。

虚拟主机配置文件在：`/usr/local/nginx/conf/vhost/域名.conf`

伪静态规则文件需要放在`/usr/local/nginx/conf/`下面。

编辑虚拟主机配置文件，可以使用 vi、nano 或 winscp，后 2 个工具对新手来说简单些。

例如前面我们添加的虚拟主机，打开后前半部分配置会显示如下：

```bash
root@riddle:~# cat /usr/local/nginx/conf/vhost/www.vpser.net.conf
server
    {
        listen 80;
        #listen [::]:80;
        server_name www.vpser.net vpser.net;
        index index.html index.htm index.php default.html default.htm default.php;
        root  /home/wwwroot/www.vpser.net;

        include rewrite/typecho.conf;
        #error_page   404   /404.html;

        # Deny access to PHP files in specific directory
        #location ~ /(wp-content|uploads|wp-includes|images)/.*\.php$ { deny all; }

        include enable-php-pathinfo.conf;

        location ~ .*\.(gif|jpg|jpeg|png|bmp|swf)$
        {
            expires      30d;
        }

        location ~ .*\.(js|css)?$
        {
            expires      12h;
        }

        location ~ /.well-known {
            allow all;
        }

        location ~ /\.
        {
            deny all;
        }

        access_log  /home/wwwlogs/www.vpser.net.log;
    }
```

在`root /home/wwwroot/www.vpser.net;`这一行下面添加：
`include wordpress.conf;`

上面的`wordpress.conf`为伪静态文件，如需要其他伪静态文件自己创建个并上传到`/usr/local/nginx/conf/`下面并`include 伪静态.conf`; 加完保存，执行：`/etc/init.d/nginx restart` 重启生效，如果报错可能是添加有误或伪静态规则有误。

1.4 及之前版本伪静态文件都在 `/usr/local/nginx/conf/` 目录下

1.5 及之后版本伪静态文件都在 `/usr/local/nginx/conf/rewrite` 目录下

伪静态文件名称后面带 2 的是二级目录的伪静态，可以根据自己需求修改里面二级目录的名称或复制为其他名字后 include 到虚拟主机配置文件中。

## 上传网站程序

如果已经[安装 FTP 服务器](http://lnmp.org/faq/ftpserver.html)可以直接使用 ftp 客户端通过你的 FTP 信息登录后上传网站或 sftp 等软件上传网站，设置好相关权限开始安装即可。

上传网站后建议执行：`chown www:www -R /path/to/dir`对网站目录进行权限设置，`/path/to/dir`替换为你网站目录。

> 为了安全可以将一些不需要 PHP 运行的上传文件之类的目录去掉执行权限，参考：http://www.vpser.net/security/lnmp-remove-nginx-php-execute.html

## 已存在虚拟主机添加 ssl 证书开启 https

对于已存在的虚拟主机添加 https 站点，可以执行：`lnmp ssl add` 命令添加 ssl 证书，目前有两种方式一种是使用自备的 ssl 证书，二是采用 Let'sEncrypt 的免费证书。添加过程和前面的添加虚拟主机的过程是一样的，只是会多一项填写 ssl 证书和 key 的步骤或直接选择 Let'sEncrypt 自动生成证书。

> 如果是`1.*版本`升级到 1.4 或更高版本的需要参考：https://lnmp.org/faq/upgrade1-4.html 中的说明.

**如果访问 https 站点时提示不安全或不显示小绿锁的话一般有以下几个原因：**

- SSL 证书可能到期；
- 网站代码里可能有 http 的资源如 css、js、图片等；一般可以在 Chrome 浏览器里按 F12 快捷键，刷新，在 Console 选项下一般都会有提示。

## 列出网站(虚拟主机)

执行：`lnmp vhost list`

```
root@riddle:~# lnmp vhost list
+-------------------------------------------+
|    Manager for LNMP, Written by Licess    |
+-------------------------------------------+
|              https://lnmp.org             |
+-------------------------------------------+
Nginx Virtualhost list:
192.168.133.128
www.vpser.net
```

## 删除网站(虚拟主机)

执行：`lnmp vhost del`

```
root@riddle:~# lnmp vhost del
+-------------------------------------------+
|    Manager for LNMP, Written by Licess    |
+-------------------------------------------+
|              https://lnmp.org             |
+-------------------------------------------+
=======================================
Current Virtualhost:
Nginx Virtualhost list:
192.168.133.128
www.vpser.net
=======================================
Please enter domain you want to delete:
```

删除网站会先列出当前已有虚拟主机，按提示输入要删除的虚拟主机域名 回车确认。

**这里只是删除虚拟主机配置文件，网站文件并不会删除需要自己删除。**

LNMP 1.2 或更高版本下需要执行：`chattr -i /网站目录/.user.ini` 后才能完整删除网站目录。

当执行 chown 或 chmod 对网站目录属主属组或权限进行操作时可能会提示

```bash
chown: changing ownership of `/home/wwwroot/default/.user.ini': Operation not permitted
```

不需要理会，如果有强迫症可以参考前面先进行`chattr -i`的操作。

## 默认网站(虚拟主机)

LNMP 默认网站配置文件：`/usr/local/nginx/conf/nginx.conf`
LNMPA 默认网站配置文件：`/usr/local/nginx/conf/nginx.conf` 和 `/usr/local/apache/conf/extra/httpd-vhosts.conf`
LAMP 默认网站配置文件：`/usr/local/apache/conf/extra/httpd-vhosts.conf`

## 防跨目录设置

LNMP 1.1 及之前的版本使用`php.ini`里面，[open_basedir 设置](http://www.vpser.net/security/lnmp-cross-site-corss-dir-security.html)

LNMP 1.2 及更高版本防跨目录功能使用`.user.ini`，该文件在网站根目录下，可以修改`.user.ini` 里面的`open_basedir`的值来设置限制访问的目录或删除来移除防跨目录的设置。

- `.user.ini`文件无法直接修改，如要修或删除需要先执行：`chattr -i /网站目录/.user.ini`
- 可以使用 winscp 文件管理、vim 编辑器或 nano 编辑器进行修改。
- 删除的话`rm -f /网站目录/.user.ini`就可以。
- 修改完成后再执行：`chattr +i /网站目录/.user.ini`
- `.user.ini`不需要重启一般 5 分钟左右生效，也可以重启一下 php-fpm 立即生效。

如果要更改网站目录必须要按上述方法修改防跨目录的设置，否则肯定报错！！

LNMP 1.4 或更高版本如果不想用防跨目录除需要删除`.user.ini`的防跨目录的目录还需要将 `/usr/local/nginx/conf/fastcgi.conf`里面的`fastcgi_param PHP_ADMIN_VALUE "open_basedir=$document_root/:/tmp/:/proc/";`在该行行前添加 # 或删除改行，需要重启 nginx。

LNMP 1.4 或更高版本也可以直接使用 lnmp 安装包 `tools/` 目录下的 `./remove_open_basedir_restriction.sh`进行移除。
在 Thinkphp、codeigniter、Laravel 等框架下，网站目录一般是在 public 下，但是 public 下的程序要跨目录调用 public 上级目录下的文件，因为 LNMP 默认是不允许跨目录访问的，所以都是必须要将防跨目录访问的设置去掉，有时候这些框架类的程序提示 500 错误也可能是这个问题引起的。

LNMPA 或 LAMP 模式 1.2 版本或更高版本的防跨目录的设置使用的对应 apache 虚拟主机配置文件（lnmp 管理工具添加的话文件是 `/usr/local/apache/conf/vhost/域名.conf`）里的`php_admin_value open_basedir`参数进行设置。如果不需要防跨目录设置可以在 `php_admin_value open_basedir`该行前面加 # 进行注释，或自行修改参数后面的目录。

重启 apache 生效。

## pathinfo 设置

LNMP 上各个版本 pathinfo 各个版本的设置基本一样：

lnmp v1.1 上，修改对应虚拟主机的配置文件(`/usr/local/nginx/conf/vhost/域名.conf`)
去掉`#include pathinfo.conf`前面的#，把`try_files $uri =404;`前面加上# 注释掉。

1.2, 1.3, 1.4, 1.5 及以上版本，修改对应虚拟主机的配置文件(`/usr/local/nginx/conf/vhost/域名.conf`)
将`include enable-php.conf;`替换为`include enable-php-pathinfo.conf;`

1.4 版本多 PHP 版本启用 pathinfo 的话，进入`/usr/local/nginx/conf`目录，拷贝一份`enable-php-pathinfo.conf`命名为`enable-php7.2-pathinfo.conf`，将 `enable-php7.2.conf`文件里 `fastcgi_pass`这一行内容完整的复制下来替换 `enable-php7.2-pathinfo.conf`文件中的 `fastcgi_pass`这一行 ，保存，再按前面的方法修改虚拟主机 `include enable-php7.2-pathinfo.conf;`就行了，其他版本以此类推。

1.5 版本多 PHP 版本开启 pathinfo 的话，可以在`lnmp vhost add` 是选择启用 pathinfo，如果存在多 PHP 版本就会提示你选择，也可以直接修改虚拟主机配置文件将`include enable-php.conf;`替换为 `include enable-php7.2-pathinfo.conf;`保存

修改 pathinfo 需要重启 nginx 生效。

## 数据库管理

1.3 以上版本，可以在添加虚拟主机时选择创建数据库，也可以单独使用 `lnmp database add`按提示添加数据库，添加的用户名和数据库名是同名的。

- 添加数据库命令：`lnmp database add`
- 编辑数据库用户密码命令：`lnmp database edit`
- 删除数据库命令：`lnmp database del`
- 列出所有数据库命令：`lnmp database list`
