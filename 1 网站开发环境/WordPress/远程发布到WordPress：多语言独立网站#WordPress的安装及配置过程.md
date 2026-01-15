
---
目录：
上一页：
下一页：
关键词：
相关链接：

---


**安装WordPress（选择英文作为缺省语言；创建数据库db_wordpress_itree_XX）**


**修改WordPress配置文件wp_config.php，加入：**

```php
///开启debug模式
define( 'WP_DEBUG', false );
//define('WP_DEBUG', true);
//define('WP_DEBUG_LOG', true);
//define('WP_DEBUG_DISPLAY', false);
///禁用历史版本(Revisions)方法
define('WP_POST_REVISIONS', false);
/* Add any custom values between this line and the "stop editing" line. */
///禁用 HTTPS 检查
///后台=》User=》Profile：If this is a development website, you can set the environment type accordingly to enable application passwords.
//define('WP_ENVIRONMENT_TYPE', 'local');
///开启A PPLICATION PASSWORDS
define('WP_APPLICATION_PASSWORDS_ENABLED', true);
```


**后台更新模板及插件**


**后台》设置》站点语言、时区**


**注意：先安装英文，以免安装日文后看不到后台日文内容！**


**然后设置admin用户的语言为英文或中文；**


**最后修改后台设置的站点语言为目标语言（如日文）**


**此时前台大部分都是目标语言（如日文），但仍有少部分为英文！如首页右下角“Blog；About”等**


**安装Loco Translate插件激活后，就都变为目标语言了**


**如果仍然有些文本未翻译，则安装多语言插件Translatepress破解版**

WordPress安装多语言插件Translatepress破解版  
[http://127.0.0.1/forum.php?mod=viewthread&tid=77](http://127.0.0.1/forum.php?mod=viewthread&tid=77)  

  
**删除示例文章Hello World（文章内容仍然为英文！与前台语言不一致）**


**后台》设置》固定链接：选文章名**


**后台》编辑用户admin》添加应用密码，并粘贴到本地和NAS知识库的多语言配置文件config_remote_post_XX.php**


**添加自动发布插件：external-json-create-or-update-post.php**


**测试本地和NAS知识库自动发布功能是否正常：**


**帖子内容页面，手动点击“远程发布到WordPress”按钮**


**定时任务CRON**


**使用Apache的mod_rewrite重定向，把**[https://ebrainbook.com/cn](https://ebrainbook.com/"%20\t%20"_blank)**解析到**[https://ebrainbook.com/](https://ebrainbook.com/cn/"%20\t%20"_blank)
在 Apache 的配置文件或 .htaccess 文件中添加以下规则：  

```apache
/wwwroot/html/ebrainbook/.htaccess

RewriteEngine On
RewriteRule ^$ /cn/ [L]
```
