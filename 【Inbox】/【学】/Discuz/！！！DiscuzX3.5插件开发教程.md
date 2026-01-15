[https://www.dz-x.net/library/plug/plugin/plugin_example.html](https://www.dz-x.net/library/plug/plugin/plugin_example.html)  
  
  
  

**插件目录结构**

![！！！DiscuzX3.5插件开发教程](https://repo.in4tree.com/2026/01/14_1768438328682.jpeg)  
  

**请务必在第一行加入**

  
  
所有与插件有关的程序，包括全部的前台程序，因全部使用外壳调用，请务必在第一行加入

1. if(!defined('IN_DISCUZ')) {
2.         exit('Access Denied');
3. }

  

后台程序第一行加入

1. if(!defined('IN_DISCUZ') || !defined('IN_ADMINCP')) {
2.         exit('Access Denied');
3. }

  
  

**插件主类文件xxx.class.php**

1. <?php
2. if(!defined('IN_DISCUZ')) {
3.     exit('Access Denied');
4. }
5. class plugin_outline {
6.     function __construct() {
7.         global $_G;
8.         // if(!$_G['uid']) {
9.         //     return;
10.         // }
11.     }
12.     ///无效！
13. //    function plugin_outline() {
14. //        global $_G;
15. //        // ...
16. //    }
17.     ///https://www.dz-x.net/library/plug/plugin/plugin_hook.html
18.     public function common() {
19.         global $_G;
20.         // ...
21.     }
22.     public function global_outline($param) {
23.         global $_G;
24.         // ...
25.     }
26.     public function discuzcode($param) {
27.         global $_G;
28.         // ...
29.     }
30.     public function avatar($param) {
31.         global $_G;
32.         // ...
33.     }
34.     public function deletethread($param) {
35.         global $_G;
36.         // ...
37.     }
38.     public function deletepost($param) {
39.         global $_G;
40.         // ...
41.     }
42. }

  
  
  

**脚本嵌入点类**

1. class plugin_identifier_CURSCRIPT extends plugin_identifier {
2.         function HookId_1() {
3.                 ......</font>
4.                 return ...;</font>
5.         }</font>
6.         function HookId_2() {
7.                 ...... </font>
8.                return ...;
9.         }</font>
10.         ......
11. }

  
  

**插件配置文件plugin_xxx.xml**

  
  

**语言包文件lang_xxx.php**

1. <?phpif(!defined('IN_DISCUZ')) {
2.     exit('Access Denied');
3. }
4. lang('plugin_xxx', 'plugin_name', '插件名称');
5. lang('plugin_xxx', 'plugin_description', '插件描述信息');
6. // 其他文本定义
7. ?>

  
  
  

**静态资源**

template/ 目录下存放插件模板。

  
  
  

**钩子**

要在插件中使用钩子，通常需要以下步骤：

1. 定义钩子处理函数：在插件的类文件中定义一个或多个函数，这些函数将在钩子点被调用。
2. 注册钩子：在插件的配置文件中注册这些钩子处理函数，指定它们应该在哪些钩子点被调用。

以下是一个简单的示例：

1. // xxx.class.php
2. class plugin_xxx {
3.     // ...
4.     // 钩子处理函数
5.     public function global_header() {
6.         // 在页面头部输出自定义内容
7.         return '<div>这是自定义头部内容</div>';
8.     }
9.     // ...
10. }

  
  
  

**常用钩子列表**

Discuz 提供了丰富的钩子点，以下是一些常用的钩子：

- global_header：在页面头部输出内容。
- global_footer：在页面底部输出内容。
- index_top：在论坛首页顶部输出内容。
- index_bottom：在论坛首页底部输出内容。
- thread_list_top：在帖子列表顶部输出内容。
- thread_list_bottom：在帖子列表底部输出内容。
- viewthread_top：在查看帖子页面顶部输出内容。
- viewthread_bottom：在查看帖子页面底部输出内容。

  

**开启插件设计模式：显示所有页面钩子**

$_config['plugindeveloper'] = 2;  
  

**插件设计助手**

![！！！DiscuzX3.5插件开发教程](https://repo.in4tree.com/2026/01/14_1768438329426.jpeg)  
![！！！DiscuzX3.5插件开发教程](https://repo.in4tree.com/2026/01/14_1768438329752.jpeg)  

**选择模块（插件在什么位置显示）：**

  
![！！！DiscuzX3.5插件开发教程](https://repo.in4tree.com/2026/01/14_1768438330052.jpeg)  
![！！！DiscuzX3.5插件开发教程](https://repo.in4tree.com/2026/01/14_1768438330348.jpeg)  
![！！！DiscuzX3.5插件开发教程](https://repo.in4tree.com/2026/01/14_1768438330655.jpeg)  
  

**注意：页面嵌入点无法嵌入插件模板！其它如个人设置等可以**

  
![！！！DiscuzX3.5插件开发教程](https://repo.in4tree.com/2026/01/14_1768438330887.jpeg)  
  

**如选个人设置模块，就必须指定插件模板文件（如memcp.htm）！否则报错：**

  
![！！！DiscuzX3.5插件开发教程](https://repo.in4tree.com/2026/01/14_1768438331146.jpeg)  
  
![！！！DiscuzX3.5插件开发教程](https://repo.in4tree.com/2026/01/14_1768438331483.jpeg)  
  
  

**插件设计助手中未列出的其它自定义模块（比如myrepeats:switch，对应文件“自定义模块.inc.php”）**

  
![！！！DiscuzX3.5插件开发教程](https://repo.in4tree.com/2026/01/14_1768438331721.jpeg)  
  

**如果URL指定调用自定义“插件:模块”，则调用“自定义模块.inc.php”文件**

  
ajaxget(\'plugin.php?id=**myrepeats:switch**&list=yes\',\'myrepeats_menu\',\'ajaxwaitid\')  
action="plugin.php?id=myrepeats:switch  
![！！！DiscuzX3.5插件开发教程](https://repo.in4tree.com/2026/01/14_1768438331933.jpeg)