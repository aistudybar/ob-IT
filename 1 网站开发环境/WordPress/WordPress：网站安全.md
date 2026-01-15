
---
目录：
上一页：
下一页：
关键词：
相关链接：

---


**【AWS服务器关闭80端口！】**

应该在安装 WordPress 前激活 HTTPS，如果在安装后再添加，可能需要更新 WordPress 设置。  
HTTPS 还可以提升网站的 Goggle PageRank。诸如 SiteGround 这类网站托管服务提供商会提供免费的 SSL 证书。  
  

**【修改WordPress网站文件的访问权限】**

**目录：750；文件：640**

1. sudo find -type d -exec chmod 750 {} \;
2. sudo find -not -type d -exec chmod 640 {} \;


**重要文件：440**

1. sudo chmod -R 440 .htaccess
2. sudo chmod -R 440 wp-config.php


**【WordPress后台#关闭注册】**


**【WordPress后台#关闭评论】**

**WP后台=》设置=》讨论：去掉“允许他人在新文章上发表评论”**


**【安装WordPress安全插件】**

**Sucuri Security**

**MalCare**

**Wordfence**


**注意：可能会禁用 WordPress 应用程序密码！导致访问REST API时出现：“HTTP 状态码错误: 401”**


**AIOSEO - Add Your WordPress Site to Google Search Console**

[https://www.wpbeginner.com/begin ... le-webmaster-tools/](https://www.wpbeginner.com/beginners-guide/how-to-add-your-wordpress-site-to-google-webmaster-tools/)  
![WordPress：网站安全](https://repo.in4tree.com/2026/01/14_1768437854396.jpeg)  
  

**【安装WordPress历史记录日志插件】**

**WP Activity Log**

![WordPress：网站安全](https://repo.in4tree.com/2026/01/14_1768437854834.jpeg)  
将能够快速跟踪 WordPress 主题、插件和核心文件的更改。如果您发现不应有权访问这些资源的用户对主题和插件进行了更改，则您可能遇到了需要调查的恶意用户。WordPress 核心文件也是如此。  
从可搜索和可过滤的日志中，您可以开始调查和解决各种形式的站点问题，例如暴力攻击、错误解决等等。  
  

**【安装WordPress备份插件】**

**UpdraftPlus: WP Backup & Migration Plugin**

定期自动备份整站，一旦网站被黑，至少有数据可以恢复。  
  

# 【参考】

十条关于 WordPress 安全性的小贴士  
[https://developer.aliyun.com/article/533983](https://developer.aliyun.com/article/533983)