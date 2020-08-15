# Typecho 搭建

## 前期准备

## 下载

下载 Typecho 最新版本，并将文件移至站点根目录：

```bash
cd /home/wwwroot/typechoblog

wget http://typecho.org/downloads/1.1-17.10.30-release.tar.gz
tar xvf 1.1-17.10.30-release.tar.gz

mv build/* .

rm -rf build
rm 1.1-17.10.30-release.tar.gz
```

## 更改站点根目录权限

```bash
# chown www:www -R /path/to/dir
chown www:www -R /home/wwwroot/typechoblog
chmod -R 755  /home/wwwroot/typechoblog
```

## 完成安装

重载 Nginx 和 php-fpm 服务：

```bash
systemctl reload nginx.service
systemctl reload php-fpm.service
```

通过浏览器访问，就可以看到 Typecho 的初始页面, 根据提示完成后续设置，即可完成安装。

## 其他设置

LNMP 安装默认目录里的文件，如：

```bash
root@riddle:/home/wwwroot/default# ll
total 96
drwxr-xr-x  3 www  www   4096 Aug 13 08:11 ./
drwxr-xr-x  4 root root  4096 Aug 15 12:30 ../
-rw-r--r--  1 www  www   3196 Aug 13 08:11 index.html
-rw-r--r--  1 www  www   5683 Aug 13 08:11 lnmp.gif
-rw-r--r--  1 www  www  20256 Aug 13 08:11 ocp.php
-rw-r--r--  1 www  www     20 Aug 13 08:11 phpinfo.php
drwxr-xr-x 14 www  www   4096 Aug 13 08:11 phpmyadmin/
-rw-r--r--  1 www  www  42609 Aug 13 08:11 p.php
-rw-r--r--  1 root root    48 Aug 13 01:26 .user.ini
```

`ocp.php`, `phpinfo.php`, `phpmyadmin/`, `p.php`, 想在新站点使用的话复制过来就行。

## 参考

- <https://www.jianshu.com/p/e15e39e90cfc>
- <https://lnmp.org/faq/lnmp-vhost-add-howto.html>
