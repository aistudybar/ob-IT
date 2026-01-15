1. <?php
2. /**
3. *        [添加H标签(add_h_tag.{modulename})] (C)2025-2099 Powered by .
4. *        Version: 1.0
5. *        Date: 2025-3-2 22:49
6. */
7. if(!defined('IN_DISCUZ')) {
8.         exit('Access Denied');
9. }
10. class plugin_add_h_tag {
11.     public function common() {
12.             global $_G;
13.         // 这里可以放置一些全局的初始化代码
14.     }
15. }
16. class plugin_add_h_tag_forum extends plugin_add_h_tag {
17.     public function post_editorctrl_left() {
18.         global $_G;

20.          // 添加自定义的JS和CSS
21.          $html = '<link rel="stylesheet" type="text/css" href="source/plugin/add_h_tag/css/add_h_tag.css" />';
22.          $html .= '<script type="text/javascript" src="source/plugin/add_h_tag/js/add_h_tag.js"></script>';
23.          return $html;
24. //         // 另一种方法：用file_get_contents读取Html文件（不建议！无法JS调试）
25. //               return file_get_contents(DISCUZ_ROOT.'source/plugin/add_h_tag/a.html');
26.     }
27. }
28. ?>

  
  
  
// source/plugin/add_h_tag/js/add_h_tag.js

1. (function() {
2.     var button = document.createElement('button');
3.     button.className = 'add_h_tag';
4.     button.innerHTML = 'H1';
5.     button.onclick = function() {
6.         var editor = document.getElementById('e_textarea');
7.         if (editor) {
8.             var selectedText = editor.value.substring(editor.selectionStart, editor.selectionEnd);
9.             var newText = '[h1]' + selectedText + '[/h1]';
10.             [color=#ff0000]//////??????赋值后，编辑器无反应！但纯文本模式下可以正常插入[/color]
11.             editor.value = editor.value.substring(0, editor.selectionStart) + newText + editor.value.substring(editor.selectionEnd);
12.         }
13.         return false;
14.     };
15.     var toolbar = document.getElementById('e_button');
16.     if (toolbar) {
17.         toolbar.appendChild(button);
18.     }
19. })();

  
  
// a.html

1. <script type="text/javascript">
2. function add_h1_tag() {
3.     var editor = typeof(FORUMEDITOR) != 'undefined' ? FORUMEDITOR : null;
4.     if (editor) {
5.         editor.exec_command('bbcode', '[h1]', '[/h1]');
6.     } else {
7.         insertText('[h1][/h1]');
8.     }
9. }
10. </script>
11. <a href="javascript:;" title="插入 H1 标签"><img src="static/image/add_h_tag.gif" alt="H1" /></a>