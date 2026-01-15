！！！远程发布到WordPress#多语言独立网站#Discuz的配置过程

httplocalhostdiscuz_pkbforum.phpmod=viewthread&tid=84

**新建数据表：pre_forum_post_lang**

1. SET NAMES utf8mb4;
2. SET FOREIGN_KEY_CHECKS = 0;
3. -- ----------------------------
4. -- Table structure for pre_forum_post_lang
5. -- ----------------------------
6. DROP TABLE IF EXISTS `pre_forum_post_lang`;
7. CREATE TABLE `pre_forum_post_lang`  (
8.   `pid` int UNSIGNED NOT NULL,
9.   `lang` tinytext CHARACTER SET ascii COLLATE ascii_general_ci NOT NULL,
10.   `lastupdate` int UNSIGNED NULL DEFAULT 0,
11.   `subject` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci NULL DEFAULT '',
12.   `message` mediumtext CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci NULL,
13.   `wp_post_id` int UNSIGNED NULL DEFAULT NULL,
14.   PRIMARY KEY (`pid` DESC, `lang`(2) DESC) USING BTREE,
15.   INDEX `index`(`pid` ASC) USING BTREE,
16.   CONSTRAINT `key` FOREIGN KEY (`pid`) REFERENCES `pre_forum_post` (`pid`) ON DELETE CASCADE ON UPDATE RESTRICT
17. ) ENGINE = InnoDB CHARACTER SET = utf8mb4 COLLATE = utf8mb4_0900_ai_ci ROW_FORMAT = Dynamic;
18. SET FOREIGN_KEY_CHECKS = 1;

注意：外键！删除post记录后自动删除所有关联的post_lang表同一pid的所有记录。  
  
  

**设置表common_settings，新添多语言字段**

  
![！！！远程发布到WordPress：多语言独立网站：Discuz的配置过程](https://repo.in4tree.com/2026/01/14_1768437488354.jpeg)  
  

**修改数据表pre_forum_forum，新添多语言字段**

  
![！！！远程发布到WordPress：多语言独立网站：Discuz的配置过程](https://repo.in4tree.com/2026/01/14_1768437488771.jpeg)  

**然后用谷歌翻译逐个填写各个字段（注意：每次论坛新建版块都必须更新pre_forum_forum数据表！）**

  
![！！！远程发布到WordPress：多语言独立网站：Discuz的配置过程](https://repo.in4tree.com/2026/01/14_1768437489017.jpeg)  

**Discuz配置文件**

**\discuz_pkb\config\config_global.php**

  
  
![！！！远程发布到WordPress：多语言独立网站：Discuz的配置过程](https://repo.in4tree.com/2026/01/14_1768437489411.jpeg)  
  

**\discuz_pkb\config\config_remote_post_en.php等**

![！！！远程发布到WordPress：多语言独立网站：Discuz的配置过程](https://repo.in4tree.com/2026/01/14_1768437489693.jpeg)  
  
  

**Discuz中计划任务Cron相关代码**

  

**\discuz_pkb\source\include\cron\cron_remote_post_to_wordpress_en.php**

  
![！！！远程发布到WordPress：多语言独立网站：Discuz的配置过程](https://repo.in4tree.com/2026/01/14_1768437489876.jpeg)  
  

**\discuz_pkb\cron_remote_post_to_wordpress_lang.inc.php**

  
![！！！远程发布到WordPress：多语言独立网站：Discuz的配置过程](https://repo.in4tree.com/2026/01/14_1768437490111.jpeg)  
  

**\discuz_pkb\remote_post_to_wordpress.inc.php**

  
![！！！远程发布到WordPress：多语言独立网站：Discuz的配置过程](https://repo.in4tree.com/2026/01/14_1768437490353.jpeg)  
  
![！！！远程发布到WordPress：多语言独立网站：Discuz的配置过程](https://repo.in4tree.com/2026/01/14_1768437490623.jpeg)  
  
  
修改[UPGRADE#贴子显示页面上方添加远程发布到WordPress按钮]  

**\discuz_pkb\remote_post_to_wordpress.php**

![！！！远程发布到WordPress：多语言独立网站：Discuz的配置过程](https://repo.in4tree.com/2026/01/14_1768437490901.jpeg)  
  

**\discuz_pkb\source\include\topicadmin\topicadmin_moderate.php**

  
![！！！远程发布到WordPress：多语言独立网站：Discuz的配置过程](https://repo.in4tree.com/2026/01/14_1768437491196.jpeg)  

**\discuz_pkb\template/default/forum/viewthread_node.htm**

![！！！远程发布到WordPress：多语言独立网站：Discuz的配置过程](https://repo.in4tree.com/2026/01/14_1768437491401.jpeg)  
  

**\discuz_pkb\source/module/forum/forum_viewthread.php**

![！！！远程发布到WordPress：多语言独立网站：Discuz的配置过程](https://repo.in4tree.com/2026/01/14_1768437491661.jpeg)