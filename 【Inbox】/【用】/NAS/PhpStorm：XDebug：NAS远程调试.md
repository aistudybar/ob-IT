PhpStorm#XDebug#NAS远程调试

http://localhost/discuz_pkb/forum.php?mod=viewthread&tid=51

（注意：#·103使用了T-Mobile无线网络，由于T-Mobile无线网络不支持DMZ，所以服务器无法访问内网主机！无法进行远程调试）  
  

**NAS控制台界面中开启XDebug模块**

  
![PhpStorm：XDebug：NAS远程调试](https://repo.in4tree.com/2026/01/14_1768437673966.jpeg)  
[http://127.0.0.1/test.php](http://127.0.0.1/test.php)  
![PhpStorm：XDebug：NAS远程调试](https://repo.in4tree.com/2026/01/14_1768437674283.jpeg)  
  
  

**注意：NAS中Apache配置文件不建议修改，以免不一致！**

  
vi /var/packages/Apache2.4/target/usr/local/etc/apache24/conf/httpd24.conf  
  
  

**NAS设置PHP配置文件**

  
  

**找到NAS上的php配置文件**

  
![PhpStorm：XDebug：NAS远程调试](https://repo.in4tree.com/2026/01/14_1768437674523.jpeg)  
  
  
cd /volume1/@appstore/PHP8.0/misc  
vi /volume1/@appstore/PHP8.0/misc/php-fpm.ini  
  

**确认已经安装了XDebug及版本和配置**

  
![PhpStorm：XDebug：NAS远程调试](https://repo.in4tree.com/2026/01/14_1768437674837.jpeg)  
  
  

**NAS修改php配置文件**

vi /volume1/@appstore/PHP8.0/misc/php-fpm.ini

找到[xdebug]，改为：

zend_extension=xdebug

xdebug.mode=debug

xdebug.start_with_request=yes

xdebug.discover_client_host=yes       #自动检测 IDE 连接，适合本地开发机IP经常变动

###xdebug.client_host仅在 discover_client_host=no 时必要。如果同时设置，则将发现主机失败时，自动选用xdebug.client_host

###xdebug.client_host不支持多个IP或通配符，它只能指定单个主机IP地址

;xdebug.client_host=127.0.0.1      #本地开发机A

xdebug.client_host=**192.168.50.38**  #本地开发机B

xdebug.client_port=9003

xdebug.idekey=PHPSTORM  # VS Code 也可以使用"VSCODE"

xdebug.log=/var/log/xdebug.log

  
  

**NAS重启Apache**

synosystemctl restart syslog-ng

  
  
  
  
  

**本地PhpStorm配置**

**新建一个项目（discuz_pkb_remote）**

![PhpStorm：XDebug：NAS远程调试](https://repo.in4tree.com/2026/01/14_1768437675085.jpeg)  
  
  

**设置Deployment添加一个Mapping**

  
![PhpStorm：XDebug：NAS远程调试](https://repo.in4tree.com/2026/01/14_1768437675312.jpeg)  
**注意：**应设置为根目录，而不要设为discuz_pkb:  
![PhpStorm：XDebug：NAS远程调试](https://repo.in4tree.com/2026/01/14_1768437675538.jpeg)  
  
  

**设置Deployment添加一个FTP Server**

如果Root Path选项目所在目录（/web/discus_pkb）：

  
![PhpStorm：XDebug：NAS远程调试](https://repo.in4tree.com/2026/01/14_1768437675788.jpeg)  
![PhpStorm：XDebug：NAS远程调试](https://repo.in4tree.com/2026/01/14_1768437676057.jpeg)  

如果Root Path选项目所在目录改为根目录：

![PhpStorm：XDebug：NAS远程调试](https://repo.in4tree.com/2026/01/14_1768437676280.jpeg)

![PhpStorm：XDebug：NAS远程调试](https://repo.in4tree.com/2026/01/14_1768437676543.jpeg)

  
  
  

**下载服务器文件**

  
![PhpStorm：XDebug：NAS远程调试](https://repo.in4tree.com/2026/01/14_1768437676827.jpeg)

如果下载成功，则说明Deployment Mapping设置正确

  
  
  

**如果没有PHPServer则，自动添加**

在浏览器打开页面：[http://127.0.0.1/test.php](http://127.0.0.1/test.php)

激活PhpStorm跟踪，弹出PHP Server设置对话框

![PhpStorm：XDebug：NAS远程调试](https://repo.in4tree.com/2026/01/14_1768437677078.jpeg)

打开设置，选PHP》Server

![PhpStorm：XDebug：NAS远程调试](https://repo.in4tree.com/2026/01/14_1768437677313.jpeg)

  
  

**[FIX#Remote debug is not enabled]**

  
![PhpStorm：XDebug：NAS远程调试](https://repo.in4tree.com/2026/01/14_1768437677518.jpeg)  

解决：远程服务器的PHP配置文件加入：

![PhpStorm：XDebug：NAS远程调试](https://repo.in4tree.com/2026/01/14_1768437677720.jpeg)