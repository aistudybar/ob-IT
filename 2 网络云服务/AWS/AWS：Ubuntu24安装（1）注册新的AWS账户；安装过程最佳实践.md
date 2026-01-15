
---
目录：
上一页：
下一页：
关键词：
相关链接：

---


**===注册新的AWS账户（可1年内免费750小时）**

![Ubuntu24安装（1）注册新的AWS账户；安装过程最佳实践](https://repo.in4tree.com/2026/01/14_1768462764604.jpeg)


**注意：可以在旧AWS账户开放共享，然后新AWS账户即可**

![Ubuntu24安装（1）注册新的AWS账户；安装过程最佳实践](https://repo.in4tree.com/2026/01/14_1768462765044.jpeg)  
  


**MFA安全登录**

![Ubuntu24安装（1）注册新的AWS账户；安装过程最佳实践](https://repo.in4tree.com/2026/01/14_1768462765283.jpeg)  


**===安装过程最佳实践**


**新建EC2实例； Associate IP；SecureCRT连接**


**更新系统软件包**

```sh
sudo apt update && sudo apt upgrade-y
```


**安装Apache2；PHP（安装常用扩展）；MariaDB（创建远程用户修改本地用户密码）**


**测试**  
![Ubuntu24安装（1）注册新的AWS账户；安装过程最佳实践](https://repo.in4tree.com/2026/01/14_1768462765503.jpeg)  
  
**http://54.148.142.35/**  
![Ubuntu24安装（1）注册新的AWS账户；安装过程最佳实践](https://repo.in4tree.com/2026/01/14_1768462765715.jpeg)  

  
**http://54.148.142.35/index.php**  
![Ubuntu24安装（1）注册新的AWS账户；安装过程最佳实践](https://repo.in4tree.com/2026/01/14_1768462765925.jpeg)  

  
**http://54.148.142.35/test.php**  
![Ubuntu24安装（1）注册新的AWS账户；安装过程最佳实践](https://repo.in4tree.com/2026/01/14_1768462766129.jpeg)  
  

**如果出现错误（如[BUG#MySQL8.0.41#PHP Fatal error:  Uncaught mysqli_sql_exception: Access deniedfor user 'root'@'localhost']），则重新安装或更换配置**


**AWS备份快照**

**snap_ubuntu_24_20250222**  

**Mount数据盘(/wwwroot)**

**创建SFTP用户sftpuser**

**安装和配置SSL**

**修改Apache根目录**

**修改数据库目录**

**安装phpMyAdmin；RAR等**