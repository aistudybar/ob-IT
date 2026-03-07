
---
目录：
上一页：
下一页：
关键词：
相关链接：

---


`sudo apt install -y php`


# **检查 PHP 版本**

`php -v`


# **安装Apache**

`sudo apt install -y libapache2-mod-php`

![Ubuntu24安装（4）安装PHP](https://repo.in4tree.com/2026/01/14_1768437227911.jpeg)  

  
## **查看PHP可用的Module

`sudo apt-cache search php8`

![Ubuntu24安装（4）安装PHP](https://repo.in4tree.com/2026/01/14_1768437228283.jpeg)  
  

# **安装常用 PHP 扩展**

`apt install -y php **libapache2-mod-phpphp-fpm** php-mysql php-xml php-mbstring php-curl php-cli php-gd php-zip php-bcmath php-intl php-soap php-bz2php-exif`

`apt install -y php-redis`

`apt install -y php-memcached`
  
`sudo apt remove -y php-fpm php-mysql php-xml php-mbstring php-curl php-cli php-gd php-zip php-bcmath php-intl php-soap php-bz2 php-exif`  
  

## **OpenSSL 扩展 (php-openssl，默认已经安装)**

`apt install -y php-openssl`

检查是否启用

`php -m | grep openssl`


## **安装mysqli 扩展(默认已经安装)**

`apt install php-mysqli`


# **？？？？？修改 PHP 配置文件（如启用extension、调整upload_max_filesize 和 post_max_size）**

vi /etc/php/8.3/apache2/php.ini


## **测试test.php**

```php
<?php
phpinfo();
```


![Ubuntu24安装（4）安装PHP](https://repo.in4tree.com/2026/01/14_1768437228594.jpeg)  

  
# **（可选）XDebug远程调试：服务器配置安装 XDebug**

`apt install -y php-xdebug`


## **检查 XDebug 是否安装**

`php -v`

![Ubuntu24安装（4）安装PHP](https://repo.in4tree.com/2026/01/14_1768437228821.jpeg)  
  

## **找到 XDebug 配置文件**

`php --ini | grep xdebug`

`vi /etc/php/8.3/cli/conf.d/20-xdebug.ini`

添加：

```php
[xdebug]

zend_extension=xdebug

xdebug.mode=debug

xdebug.start_with_request=yes

xdebug.discover_client_host=yes       #自动检测 IDE 连接，适合本地开发机IP经常变动

###xdebug.client_host仅在 discover_client_host=no 时必要。如果同时设置，则将发现主机失败时，自动选用xdebug.client_host

###xdebug.client_host不支持多个IP或通配符，它只能指定单个主机IP地址

;xdebug.client_host=127.0.0.1      #本地开发机A

xdebug.client_host=172.59.160.114  #本地开发机B

xdebug.client_port=9003

xdebug.idekey=PHPSTORM  # VS Code 也可以使用"VSCODE"

xdebug.log=/var/log/xdebug.log
```


## **注意：在 XDebug 3.0 及以上版本（当前最新版本），xdebug.remote_host已被移除，取而代之的是 xdebug.client_host**


## **查看XDebug日志**

`vi /var/log/xdebug.log`


## **确保远程服务器允许 9003 端口入站**

`ufw allow 9003/tcp`


## **？？？XDebug远程调试：本地开发机PHPStorm配置新建一个PHPStorm项目（名为remote）**

![Ubuntu24安装（4）安装PHP](https://repo.in4tree.com/2026/01/14_1768437229102.jpeg)  
![Ubuntu24安装（4）安装PHP](https://repo.in4tree.com/2026/01/14_1768437229309.jpeg)  

  
## **打开设置，选PHP》Server，添加一个server（名为remote server）**

![Ubuntu24安装（4）安装PHP](https://repo.in4tree.com/2026/01/14_1768437229501.jpeg)  


## **添加Deployment Mapping**

![Ubuntu24安装（4）安装PHP](https://repo.in4tree.com/2026/01/14_1768437229722.jpeg)  
![Ubuntu24安装（4）安装PHP](https://repo.in4tree.com/2026/01/14_1768437229940.jpeg)  
  

## **配置SSH Configuration**

![Ubuntu24安装（4）安装PHP](https://repo.in4tree.com/2026/01/14_1768437230219.jpeg)  
![Ubuntu24安装（4）安装PHP](https://repo.in4tree.com/2026/01/14_1768437230551.jpeg)  

  
## **开始Validate**

![Ubuntu24安装（4）安装PHP](https://repo.in4tree.com/2026/01/14_1768437230812.jpeg)  


## **？？？出现如下错误，说明无法进行远程调试（T-Mobile无线网络不支持DMZ！外界无法访问内网主机！）**

![Ubuntu24安装（4）安装PHP](https://repo.in4tree.com/2026/01/14_1768437231048.jpeg)  
![Ubuntu24安装（4）安装PHP](https://repo.in4tree.com/2026/01/14_1768437231322.jpeg)  
  

## **检查日志确定XDebug是否成功**

`tail -f /var/log/xdebug.log`
