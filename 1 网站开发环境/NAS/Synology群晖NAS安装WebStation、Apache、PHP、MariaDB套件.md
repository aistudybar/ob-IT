
---
目录：
上一页：
下一页：
关键词：
相关链接：

---


**安装WebStation及Apache2.4、PHP8.0等套件**

![Synology群晖NAS安装WebStation、Apache、PHP、MariaDB套件](https://repo.in4tree.com/2026/01/14_1768437709560.jpeg)  


**NAS控制台界面中WebStation开启XDebug模块及其它扩展extensions**

  
![Synology群晖NAS安装WebStation、Apache、PHP、MariaDB套件](https://repo.in4tree.com/2026/01/14_1768437709942.jpeg)  
  

  
**注意：NAS中Apache配置文件不建议修改，以免不一致！**

`vi /var/packages/Apache2.4/target/usr/local/etc/apache24/conf/httpd24.conf  `
  

**找到NAS上的php配置文件**
  
![Synology群晖NAS安装WebStation、Apache、PHP、MariaDB套件](https://repo.in4tree.com/2026/01/14_1768437710203.jpeg)  
  
  
cd /volume1/@appstore/PHP8.0/misc  
vi /volume1/@appstore/PHP8.0/misc/php-fpm.ini  
  
  
NAS重启Apache

synosystemctl restart syslog-ng


**安装MariaDB 10套件**


**使用远程电脑的Navicat访问数据先添加数据库远程root用户，并赋予权限**

[http://192.168.50.250/phpmyadmin](http://192.168.50.250/phpmyadmin)  
**(MariaDB数据库用户名密码：root、A_wxxx4)**

![Synology群晖NAS安装WebStation、Apache、PHP、MariaDB套件](https://repo.in4tree.com/2026/01/14_1768437710467.jpeg)


**启用数据库远程访问**

![Synology群晖NAS安装WebStation、Apache、PHP、MariaDB套件](https://repo.in4tree.com/2026/01/14_1768437710725.jpeg)


**连接成功**

![Synology群晖NAS安装WebStation、Apache、PHP、MariaDB套件](https://repo.in4tree.com/2026/01/14_1768437710952.jpeg)


**开启SSH**

![Synology群晖NAS安装WebStation、Apache、PHP、MariaDB套件](https://repo.in4tree.com/2026/01/14_1768437711179.jpeg)  
  

**开启FTP**

![Synology群晖NAS安装WebStation、Apache、PHP、MariaDB套件](https://repo.in4tree.com/2026/01/14_1768437711446.jpeg)