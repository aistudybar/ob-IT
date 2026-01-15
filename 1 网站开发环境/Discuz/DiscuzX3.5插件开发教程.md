
---
目录：
上一页：
下一页：
关键词：
相关链接：

---

# [插件开发实例](https://www.dz-x.net/library/plug/plugin/plugin_example.html)

**插件目录结构**

![！！！DiscuzX3.5插件开发教程](https://repo.in4tree.com/2026/01/14_1768438328682.jpeg)  
  

## 请务必在第一行加入

所有与插件有关的程序，包括全部的前台程序，因全部使用外壳调用，请务必在第一行加入

```php
if(!defined('IN_DISCUZ')) {
        exit('Access Denied');
}
```


后台程序第一行加入

```php
if(!defined('IN_DISCUZ') || !defined('IN_ADMINCP')) {
        exit('Access Denied');
}
```

 
## 插件主类文件xxx.class.php

```php
<?php
if(!defined('IN_DISCUZ')) {
    exit('Access Denied');
}
class plugin_outline {
    function __construct() {
        global $_G;
        // if(!$_G['uid']) {
        //     return;
         // }
     }
     ///无效！
 //    function plugin_outline() {
 //        global $_G;
 //        // ...
 //    }
    ///https://www.dz-x.net/library/plug/plugin/plugin_hook.html
    public function common() {
        global $_G;
        // ...
    }
    public function global_outline($param) {
        global $_G;
        // ...
    }
    public function discuzcode($param) {
        global $_G;
        // ...
    }
    public function avatar($param) {
        global $_G;
        // ...
    }
    public function deletethread($param) {
        global $_G;
        // ...
    }
    public function deletepost($param) {
        global $_G;
        // ...
    }
}
```


## 脚本嵌入点类

```php
class plugin_identifier_CURSCRIPT extends plugin_identifier {
	function HookId_1() {
			......</font>
			return ...;</font>
	}</font>
	function HookId_2() {
			...... </font>
		   return ...;
	}</font>
	 ......
}
```


## 插件配置文件plugin_xxx.xml


## 语言包文件lang_xxx.php

```php
<?phpif(!defined('IN_DISCUZ')) {
    exit('Access Denied');
}
lang('plugin_xxx', 'plugin_name', '插件名称');
lang('plugin_xxx', 'plugin_description', '插件描述信息');
// 其他文本定义
?>
```


## 静态资源

template/ 目录下存放插件模板。


## 钩子

要在插件中使用钩子，通常需要以下步骤：

1. 定义钩子处理函数：在插件的类文件中定义一个或多个函数，这些函数将在钩子点被调用。
2. 注册钩子：在插件的配置文件中注册这些钩子处理函数，指定它们应该在哪些钩子点被调用。

以下是一个简单的示例：

```php
// xxx.class.php
class plugin_xxx {
    // ...
    // 钩子处理函数
    public function global_header() {
        // 在页面头部输出自定义内容
        return '<div>这是自定义头部内容</div>';
    }
    // ...
}
```


## 常用钩子列表

Discuz 提供了丰富的钩子点，以下是一些常用的钩子：

- global_header：在页面头部输出内容。
- global_footer：在页面底部输出内容。
- index_top：在论坛首页顶部输出内容。
- index_bottom：在论坛首页底部输出内容。
- thread_list_top：在帖子列表顶部输出内容。
- thread_list_bottom：在帖子列表底部输出内容。
- viewthread_top：在查看帖子页面顶部输出内容。
- viewthread_bottom：在查看帖子页面底部输出内容。


## 开启插件设计模式：显示所有页面钩子

$_config['plugindeveloper'] = 2;  

## 插件设计助手

![！！！DiscuzX3.5插件开发教程](https://repo.in4tree.com/2026/01/14_1768438329426.jpeg)  
![！！！DiscuzX3.5插件开发教程](https://repo.in4tree.com/2026/01/14_1768438329752.jpeg)  


## 选择模块（插件在什么位置显示）：

![！！！DiscuzX3.5插件开发教程](https://repo.in4tree.com/2026/01/14_1768438330052.jpeg)  
![！！！DiscuzX3.5插件开发教程](https://repo.in4tree.com/2026/01/14_1768438330348.jpeg)  
![！！！DiscuzX3.5插件开发教程](https://repo.in4tree.com/2026/01/14_1768438330655.jpeg)  


## 注意：页面嵌入点无法嵌入插件模板！其它如个人设置等可以

![！！！DiscuzX3.5插件开发教程](https://repo.in4tree.com/2026/01/14_1768438330887.jpeg)  


## 如选个人设置模块，就必须指定插件模板文件（如memcp.htm）！否则报错：

![！！！DiscuzX3.5插件开发教程](https://repo.in4tree.com/2026/01/14_1768438331146.jpeg)  
  
![！！！DiscuzX3.5插件开发教程](https://repo.in4tree.com/2026/01/14_1768438331483.jpeg)  


## 插件设计助手中未列出的其它自定义模块（比如myrepeats:switch，对应文件“自定义模块.inc.php”）
  
![！！！DiscuzX3.5插件开发教程](https://repo.in4tree.com/2026/01/14_1768438331721.jpeg)  


## 如果URL指定调用自定义“插件:模块”，则调用“自定义模块.inc.php”文件

ajaxget(\'plugin.php?id=**myrepeats:switch**&list=yes\',\'myrepeats_menu\',\'ajaxwaitid\')  
action="plugin.php?id=myrepeats:switch  
![！！！DiscuzX3.5插件开发教程](https://repo.in4tree.com/2026/01/14_1768438331933.jpeg)