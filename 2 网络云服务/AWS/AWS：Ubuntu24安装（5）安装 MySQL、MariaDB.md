
---
目录：
上一页：
下一页：
关键词：
相关链接：

---

# ===安装 MariaDB

sudo apt install mariadb-server -y


**查看运行状态**

sudo systemctl status mariadb


**重新启动**

sudo systemctl restart mariadb

sudo systemctl start mariadb

sudo systemctl stop mariadb


**开机自启**

sudo systemctl enable mariadb


**（可选）运行安全脚本**

sudo mysql_secure_installation


**配置文件（修改端口）**

vi /etc/mysql/mariadb.conf.d/50-server.cnf

![Ubuntu24安装（5）安装 MySQL、MariaDB](https://repo.in4tree.com/2026/01/14_1768437251579.jpeg)  

  
**进入MySQL命令行，添加远程用户root（含密码）**

mysql -u root -p

mysql> CREATE USER 'root'@'%' IDENTIFIEDBY 'weiwei2544';

mysql> GRANTALL PRIVILEGES ON*.* TO 'root'@'%' WITH GRANT OPTION;

mysql> FLUSH PRIVILEGES;


**修改MySQL用户的密码**

mysql -u root -p

mysql> ALTERUSER 'root'@'localhost' IDENTIFIED BY 'weiwei2544';

mysql> FLUSHPRIVILEGES;


**允许远程连接**

**编辑配置文件**

vi /etc/mysql/mariadb.conf.d/50-server.cnf  
![Ubuntu24安装（5）安装 MySQL、MariaDB](https://repo.in4tree.com/2026/01/14_1768437251885.jpeg)


**修改数据库目录**

sudo systemctl stop mariadb


**修改配置文件**

vi /etc/mysql/mariadb.conf.d/50-server.cnf

![Ubuntu24安装（5）安装 MySQL、MariaDB](https://repo.in4tree.com/2026/01/14_1768437252117.jpeg)  

  
**复制数据库**

mkdir -p /wwwroot/lib/mysql/

sudo rsync -av /var/lib/mysql/ /wwwroot/lib/mysq/

mv /var/lib/mysql/ /wwwroot/lib/mysq/


**？？？如果启用了AppArmor，更新其配置以允许 MariaDB 访问新目录**

vi /etc/apparmor.d/tunables/alias

添加

alias /var/lib/mysql/ -> /wwwroot/lib/mysql/,

![Ubuntu24安装（5）安装 MySQL、MariaDB](https://repo.in4tree.com/2026/01/14_1768437252374.jpeg)  

vi /etc/apparmor.d/usr.sbin.mysqld

/wwwroot/lib/mysql/ r,

/wwwroot/lib/mysql/** rwk,

![Ubuntu24安装（5）安装 MySQL、MariaDB](https://repo.in4tree.com/2026/01/14_1768437252581.jpeg)  

  
vi /etc/apparmor.d/abstractions/mysql

![Ubuntu24安装（5）安装 MySQL、MariaDB](https://repo.in4tree.com/2026/01/14_1768437252818.jpeg)  
  

然后重新加载 AppArmor

systemctl restart apparmor


**修改 MySQL systemd 服务MySQL 的 systemd 可能会忽略 mysqld.cnf 配置，需要手动指定 datadir：**

sudo systemctl edit mysql添加：  
[Service]ExecStart=ExecStart=/usr/sbin/mysqld --datadir=/wwwroot/lib/mysql保存后，重新加载 systemd：  
sudo systemctl daemon-reload  

  
**清理旧数据（可选）**

sudo rm -rf /var/lib/mysql/


**安装phpMyAdmin**

aptinstall phpMyAdmin -y


**配置 ApachephpMyAdmin 可能没有自动配置 Apache，因此你需要手动创建一个配置文件：**

sudo nano/etc/apache2/conf-available/phpmyadmin.conf

Alias /phpmyadmin /usr/share/phpmyadmin

```apache
<Directory /usr/share/phpmyadmin>

   Options SymLinksIfOwnerMatch

   DirectoryIndex index.php

   <IfModule mod_php.c>

       <FilesMatch ".+\.php$">

           SetHandler application/x-httpd-php

       </FilesMatch>

       php_admin_value upload_max_filesize 50M

       php_admin_value post_max_size 50M

       php_admin_value max_execution_time 300

       php_admin_value max_input_time 300

   </IfModule>

   Require all granted

</Directory>
```


**建立软链到/wwwroot/html/ibrainbook**

sudo ln -s /usr/share/phpmyadmin /wwwroot/html/ibrainbook/phpMyAdmin


**启用phpmyadmin配置**

sudoa2enconf phpmyadmin

sudosystemctl reload apache2

![Ubuntu24安装（5）安装 MySQL、MariaDB](https://repo.in4tree.com/2026/01/14_1768437253022.jpeg)  

  
**（可选）修改phpMyAdmin配置**

phpMyAdmin默认也不允许空密码登录。你需要修改其配置文件以允许空密码

nano/etc/phpmyadmin/config.inc.php


**导出数据库数据**

mysqldump-u [user] -p [db_name] > [export_the_db.sql]


# **===（放弃！有BUG！）安装MySQL**

Ubuntu 24.04 的默认软件仓库包含 MySQL，因此可以直接安装

sudo apt install mysql-server -y


**查看运行状态**

systemctl status mysql.service

![Ubuntu24安装（5）安装 MySQL、MariaDB](https://repo.in4tree.com/2026/01/14_1768437253239.jpeg)  
  

**重启MySQL**

service mysql restart

service mysql start

service mysql stop


**MySQL 开机自启**

systemctl enablemysql


**获取版本**

apt list --installed \\ | grep -E 'mysql-(client\\ | server)'

![Ubuntu24安装（5）安装 MySQL、MariaDB](https://repo.in4tree.com/2026/01/14_1768437253524.jpeg)  

  
**查看数据目录**

mysql -u root -p -e "SELECT@@datadir;"

![Ubuntu24安装（5）安装 MySQL、MariaDB](https://repo.in4tree.com/2026/01/14_1768437253758.jpeg)  
  

**查看MySQL错误日志**

cat /var/log/mysql/error.log


**（可选）运行安全配置向导**

sudo mysql_secure_installation

根据提示进行以下操作：

- 设置 root 用户密码（如果有提示）
- 移除匿名用户 (建议选择 Y)
- 禁止 root 远程登录 (因需要远程管理，选择 N)
- 移除测试数据库 (建议选择 Y)
- 重新加载权限表 (选择 Y)


**进入MySQL命令行，添加远程用户root（含密码）**

mysql -u root -p

mysql> CREATE USER 'root'@'%' IDENTIFIEDBY 'weiwei2544';

mysql> GRANTALL PRIVILEGES ON*.* TO 'root'@'%' WITH GRANT OPTION;

mysql> FLUSH PRIVILEGES;


**修改MySQL用户的密码**

mysql -u root -p

mysql> ALTERUSER 'root'@'localhost' IDENTIFIED BY 'weiwei2544';

mysql> FLUSHPRIVILEGES;


**配置文件，允许远程连接**

vi /etc/mysql/mysql.conf.d/mysqld.cnf

找到以下行：

bind-address = 127.0.0.1

改成：

bind-address = 0.0.0.0


**(可选) 允许MySQL 端口（默认 3306，3399）通过防火墙**

sudo ufw allow 3306/tcp

sudo ufw allow 3399/tcp

![Ubuntu24安装（5）安装 MySQL、MariaDB](https://repo.in4tree.com/2026/01/14_1768437253987.jpeg)  

  
**（可选）编辑MySQL配置文件，修改数据库目录**

！！！[https://blog.csdn.net/qq_33187368/article/details/129832763](https://blog.csdn.net/qq_33187368/article/details/129832763)

vi /etc/mysql/mysql.conf.d/mysqld.cnf

![Ubuntu24安装（5）安装 MySQL、MariaDB](https://repo.in4tree.com/2026/01/14_1768437254193.jpeg)  

  
**停止MySQL**

sudo systemctl stop mysql


**复制数据库数据**

rsync -av /var/lib/mysql/ /wwwroot/lib/mysql/

为防止误操作，可以先备份旧目录

rm -R /var/lib/mysql.bak

mv /var/lib/mysql /var/lib/mysql.bak

mv /var/lib/mysql.bak /var/lib/mysq


**配置 AppArmor 规则Ubuntu 使用 AppArmor 限制 MySQL 访问特定目录，所以必须修改规则。**

vi /etc/apparmor.d/tunables/alias

添加

alias /var/lib/mysql/ -> /wwwroot/lib/mysql/,

![Ubuntu24安装（5）安装 MySQL、MariaDB](https://repo.in4tree.com/2026/01/14_1768437254418.jpeg)  

vi /etc/apparmor.d/usr.sbin.mysqld

![Ubuntu24安装（5）安装 MySQL、MariaDB](https://repo.in4tree.com/2026/01/14_1768437254640.jpeg)  

vi /etc/apparmor.d/abstractions/mysql

![Ubuntu24安装（5）安装 MySQL、MariaDB](https://repo.in4tree.com/2026/01/14_1768437254931.jpeg)  
  

然后重新加载 AppArmor

systemctl restart apparmor


**修改 MySQL systemd 服务MySQL 的 systemd 可能会忽略 mysqld.cnf 配置，需要手动指定 datadir：**

sudo systemctl edit mysql添加：  
[Service]ExecStart=ExecStart=/usr/sbin/mysqld --datadir=/wwwroot/lib/mysql保存后，重新加载 systemd：  
sudo systemctl daemon-reload  

  
**修复权限并启动 MySQL**

chown -R mysql:mysql /wwwroot/lib

sudo systemctl start mysql

sudo systemctl status mysql

![Ubuntu24安装（5）安装 MySQL、MariaDB](https://repo.in4tree.com/2026/01/14_1768437255213.jpeg)  

  
# **===[BUG#MySQL8.0.41#PHP Fatal error:  Uncaught mysqli_sql_exception: Access deniedfor user 'root'@'localhost']**

服务器：Ubuntu24.04; PHP8.3.6;MySQL8.0.41

cat /var/log/apache2/error.log

![Ubuntu24安装（5）安装 MySQL、MariaDB](https://repo.in4tree.com/2026/01/14_1768437255477.jpeg)  

MySQLi服务器PHP8.3.6P# 远程访问数据库127.0.0.1.# =》失败！SQLSTATE[HY000] [1698] Access deniedfor user 'root'@'localhost'

MySQLi：本地PHP8.4.4# 远程访问数据库54.148.142.35# =》 OK！

MySQLi：服务器PHP8.3.6# 远程访问数据库54.148.142.35# =》失败！

PDO：本地PHP8.4.4# 远程访问数据库54.148.142.35# =》OK！

PDO：服务器PHP8.3.6# 远程访问数据库54.148.142.35# =》失败！连接失败: SQLSTATE[HY000] [2002] Connection timed out

PDO：服务器PHP8.3.6# 远程访问数据库127.0.0.1.# =》失败！SQLSTATE[HY000] [1698] Access deniedfor user 'root'@'localhost'

换Ubuntu各版本和PHP各版本后问题依旧！

AWS Linux 2023+MySQL8则正常


**结论：Ubuntu 24，无论是否移动数据库目录或网站根目录，只要PHP代码在服务器用127.0.0.1访问数据库，就出现该错误！暂时解决：放弃MySQL！使用MariaDB即可**
|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |