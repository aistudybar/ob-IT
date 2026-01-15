
---
目录：
上一页：
下一页：
关键词：
相关链接：

---



**下载安装配置PHP**

**注意：最新Xdebug、Synology要求8.0以上版本，推荐PHP 8.4！**

![搭建Windows网站开发环境：安装PHP8.4](https://repo.in4tree.com/2026/01/14_1768438099718.jpeg)  


**选择ThreadSafe**

![搭建Windows网站开发环境：安装PHP8.4](https://repo.in4tree.com/2026/01/14_1768438100174.jpeg)  

**将php.ini-development改名为php.ini,并修改内容（扩展所在目录等）**

```php
extension_dir = "D:/php84/ext"
session.save_path = "D:/php84/tmp"
```


**查看php版本**

`php -v`


**Installation for Apache 2.x on Windows systems**

[https://www.php.net/manual/en/install.windows.apache2.php#install.windows.apache2](https://www.php.net/manual/en/install.windows.apache2.php#install.windows.apache2)

There are three ways to set up PHP to work with Apache 2.x on Windows. PHP can be run as a handler, as a CGI, or under FastCGI.


**推荐Handle即模块方式（要求PHP Thread-Safe！）**
[https://ntflc.com/2017/06/04/Install-Apache-and-PHP-on-Windows/](https://ntflc.com/2017/06/04/Install-Apache-and-PHP-on-Windows/)


**Apache添加 PHP 模块**

在 Apache 配置文件 D:\Apache24\conf\httpd.conf 的 180 行左右（即一堆 #LoadModule xxx 后）添加：

```apache
PHPIniDir "D:/php84"
LoadModule php7_module "D:/php84/php7apache2_4.dll"
```


**添加 PHP 文件后缀**

在 Apache 配置文件 D:\Apache24\conf\httpd.conf 的 393 行左右，即：

<IfModule mime_module>

    TypesConfig conf/mime.types

    ....

</IfModule>

之间，添加 AddType application/x-httpd-php .php。即：

<IfModule mime_module>

    TypesConfig conf/mime.types

    ....

   **AddType application/x-httpd-php .php**

</IfModule>


**添加主页 index.php**

在 Apache 配置文件 D:\Apache24\conf\httpd.conf 的 278 行左右，即：

<IfModule dir_module>

    DirectoryIndex index.html

</IfModule>

中，在 index.html 前添加 index.php。即：

<IfModule dir_module>

   **DirectoryIndex index.php index.html**

</IfModule>


**测试效果**

创建 index.php：

```php
<?php
echo phpinfo();
```