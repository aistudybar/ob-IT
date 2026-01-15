
---
目录：
上一页：
下一页：
关键词：
相关链接：

---


> 注意：wordpress.org下载，wordpress.com托管服务  

**WordPress安装方法分为虚拟主机上安装和VPS上安装，两者的方法是不一样的，不同虚拟主机安装方法也不同，本文为常规WordPress安装教程**


**下载WordPress**

[https://wordpress.org/download/](https://wordpress.org/download/)


**安装Wordpress**

http://localhost/wordpress

![安装配置WordPress开发环境](https://repo.in4tree.com/2026/01/14_1768438019128.jpeg)


**先建立MySQL数据库：比如db_wordpress**

![安装配置WordPress开发环境](https://repo.in4tree.com/2026/01/14_1768438019546.jpeg)

![安装配置WordPress开发环境](https://repo.in4tree.com/2026/01/14_1768438019763.jpeg)

![安装配置WordPress开发环境](https://repo.in4tree.com/2026/01/14_1768438019970.jpeg)


**配置WordPress开启debug模式**

**wp-config.php：**

```php
define('WP_DEBUG', true);
define('WP_DEBUG_LOG',true);
define('WP_DEBUG_DISPLAY', false);
```


**LOG文件：**

`wp-content/debug.log`


**调试代码：**

`error_log('rest_api_init triggered'); ///写入日志`


**后台设置Permalink**

**注意：PHP确保开启mode_rewrite**

**修改Apache配置httpd.conf并搜索：'LoadModule rewrite_module modules/mod_rewrite.so'**

并将Directory "D:/wwwroot"的AllowOverride替换为**All**

重启Apache后生效

`phpinfo()会找到‘rewrite_module’  `
  

**WordPress后台更新Permalink后，能自动生成.htaccess（但无论选哪一项，都生成一样的内容！）**

**在WordPress 6上，无需URL Rewrite更改您的Permalink**

比如：  
[http://example.com/?rest_route=/wp/v2/posts](http://example.com/?rest_route=/wp/v2/posts)  
[http://example.com/index.php?rest_route=/wp/v2/posts](http://example.com/index.php?rest_route=/wp/v2/posts)  

  
**WordPress后台Permalink设置失效问题：无index.php或?p=XXX则404：**

修改Apache配置，将Directory "D:/wwwroot"的AllowOverride替换为All，重启后生效  

```php
/// http://localhost/wordpress_itree/index.php?rest_route=/ （rest_route映射为wp-json）  
/// http://localhost/wordpress_itree/index.php?rest_route=/wp-json （返回#404！rest_route映射为wp-json）  
/// http://localhost/wordpress_itree/index.php?rest_route=/wp/v2  
/// http://localhost/wordpress_itree/index.php?rest_route=/external-json/v1 （{"namespace":"external-json\/v1）  
/// http://localhost/wordpress_itree/index.php?rest_route=/external-json/v1/create-post （返回#404！create-post是节点，而不是路径）  
/// http://localhost/wordpress_itree/index.php/wp-json （当后台设置'Permalink为/index.php/%postname%/'时ok！）
```
  

**搭建好WordPress网站后的基本操作流程**

1.    设置网站SSL安全证书；（部分虚拟主机会自动设置，也可以后期再安装，SSL证书有免费的，不需要单独购买。）

2.    进入设置里面设置Permalink固定链接；[WordPress Permalink路由](http://localhost/discuz_pkb/forum.php?mod=viewthread&tid=11)

3.   进入文章 – 分类目录，设置文章分类；

4.   进入外观 – 主题，里面挑选一个自己喜欢的主题；（如果是外贸网站，建议直接到[themeforset](https://1.envato.market/We2DO)购买付费主题使用。）

5.   进入插件，安装自己需要用到的一些插件，例如SEO插件、缓存插件；

6.   SEO优化


**访问网站后台：网址后面添加 `/wp-admin`**