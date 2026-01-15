
---
目录：
上一页：
下一页：
关键词：
相关链接：

---

```php
<?php
/**
*        [添加H标签(add_h_tag.{modulename})] (C)2025-2099 Powered by .
*        Version: 1.0
*        Date: 2025-3-2 22:49
*/
if(!defined('IN_DISCUZ')) {
        exit('Access Denied');
}
 class plugin_add_h_tag {
     public function common() {
             global $_G;
         // 这里可以放置一些全局的初始化代码
     }
 }
 class plugin_add_h_tag_forum extends plugin_add_h_tag {
     public function post_editorctrl_left() {
         global $_G;

          // 添加自定义的JS和CSS
          $html = '<link rel="stylesheet" type="text/css" href="source/plugin/add_h_tag/css/add_h_tag.css" />';
          $html .= '<script type="text/javascript" src="source/plugin/add_h_tag/js/add_h_tag.js"></script>';
          return $html;
 //         // 另一种方法：用file_get_contents读取Html文件（不建议！无法JS调试）
 //               return file_get_contents(DISCUZ_ROOT.'source/plugin/add_h_tag/a.html');
    }
}
?>
```


// source/plugin/add_h_tag/js/add_h_tag.js
```php
(function() {
    var button = document.createElement('button');
    button.className = 'add_h_tag';
    button.innerHTML = 'H1';
    button.onclick = function() {
        var editor = document.getElementById('e_textarea');
        if (editor) {
            var selectedText = editor.value.substring(editor.selectionStart, editor.selectionEnd);
            var newText = '[h1]' + selectedText + '[/h1]';
             [color=#ff0000]//////??????赋值后，编辑器无反应！但纯文本模式下可以正常插入[/color]
             editor.value = editor.value.substring(0, editor.selectionStart) + newText + editor.value.substring(editor.selectionEnd);
         }
         return false;
     };
     var toolbar = document.getElementById('e_button');
     if (toolbar) {
         toolbar.appendChild(button);
     }
})();
```


// a.html
```php
<script type="text/javascript">
function add_h1_tag() {
    var editor = typeof(FORUMEDITOR) != 'undefined' ? FORUMEDITOR : null;
    if (editor) {
        editor.exec_command('bbcode', '[h1]', '[/h1]');
    } else {
        insertText('[h1][/h1]');
    }
}
</script>
<a href="javascript:;" title="插入 H1 标签"><img src="static/image/add_h_tag.gif" alt="H1" /></a>
```

