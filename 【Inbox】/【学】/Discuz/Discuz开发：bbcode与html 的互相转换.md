$str = "<b><i>的的顶顶顶顶顶的顶顶顶顶顶顶顶顶顶的的</i></b>";

  

**html转成bbcode**

require_once libfile('function/editor');

echo html2bbcode($str);

echo "</br>";

$str2 = '**_的的顶顶顶顶顶的顶顶顶顶顶顶顶顶顶的的_**';

  

**将bbcode转成html**

require_oncelibfile('function/discuzcode');

echo discuzcode($str2, 0, 0, 0, 1, 1, 0, 0,0, 0, 0);

  
  

**在线工具：BBCode转HTML**

[https://www.lzltool.com/Tools/BbcodeToHtml](https://www.lzltool.com/Tools/BbcodeToHtml)