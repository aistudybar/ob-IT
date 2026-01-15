Ubuntu 24.04安装WordPress

http://localhost/discuz_pkb/forum.php?mod=viewthread&tid=75

**注意：事先安装好Apache+PHP+MySQL**

  

**更新系统**

**sudo apt update && sudo apt upgrade -y**

  
  

**创建 WordPress 数据库（如db_wordpress_itree）**

  
  
  

**前往 /wwwroot/html/ebrainbook目录并下载最新版本的 WordPress：**

  
cd /wwwroot/html/ebrainbook  
sudo wget [https://wordpress.org/latest.tar.gz](https://wordpress.org/latest.tar.gz)  
sudo tar -xzvf latest.tar.gz  
sudo rm latest.tar.gz  
  

**将解压后的文件移动到正确的位置并设置权限**

  
  
sudo mv wordpress/* .  
sudo rm -r wordpress  
sudo chown -R www-data:www-data /wwwroot/html/ebrainbook  
网站目录权限为750，网站文件权限为640，个别目录设置可写权限770  
参考：网站目录读写权限的设置  
[http://127.0.0.1/forum.php?mod=viewthread&tid=27](http://127.0.0.1/forum.php?mod=viewthread&tid=27)  
(出处: 知识库)  
  
  

**配置 WordPress 数据库连接**

  
  
sudo cp wp-config-sample.php wp-config.php  
sudo nano wp-config.php  
  
  
  

**浏览器打开网站**

  
![Ubuntu 24.04安装WordPress](https://repo.in4tree.com/2026/01/14_1768437060772.jpeg)  

**修改配置文件：wp_config.php**

  
![Ubuntu 24.04安装WordPress](https://repo.in4tree.com/2026/01/14_1768437061510.jpeg)  
  
  

**配置WordPress**

  

**WordPress后台更新永久固定链接Permalink：**

  
![Ubuntu 24.04安装WordPress](https://repo.in4tree.com/2026/01/14_1768437062018.jpeg)  

**验证永久固定链接Permalink：[https://ebrainbook.com/wp-json/](https://ebrainbook.com/wp-json/"%20\t%20"_blank)**

  
应输出内容，而不是404错误！  
![Ubuntu 24.04安装WordPress](https://repo.in4tree.com/2026/01/14_1768437062806.jpeg)  
  

**如果出现404错误，而“**[**https://ebrainbook.com/index.php?rest_route=/**](https://ebrainbook.com/index.php?rest_route=/)**”正常，则修改Apache配置文件：**

**1）确保Apache已经安装mod_rewrite**

  
2）修改AllowOverride为All：  
![Ubuntu 24.04安装WordPress](https://repo.in4tree.com/2026/01/14_1768437063236.jpeg)  
  

**设置用户（如admin）的Application Password**

![Ubuntu 24.04安装WordPress](https://repo.in4tree.com/2026/01/14_1768437063514.jpeg)  

**注意：如果出现错误（如：Not found），则可能永久固定链接Permalink没有设置成功。**