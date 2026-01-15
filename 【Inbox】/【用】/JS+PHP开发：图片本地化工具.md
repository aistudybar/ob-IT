
---
目录：
上一页：
下一页：
关键词：
相关链接：

---

**【描述】**

更快捷方便地添加图片到知识库（Discuz bbcode富文本编辑器），提高手工发帖速度和效率。

比如远程图片、剪切板中Base64图片等。

  
  
  

**【注意】不用****node.js****或****JS****的****fetch(****远程****url)****！（****fetch(****本地****url)****正常），因存在****CORS****跨域问题【注意】因要求****https****，无法实现点击按钮来获取剪切板内容！****https****问题的解决方法：**

  
  

·         部署到     https:// 站点运行（如 GitHub Pages、Vercel、Netlify）。

·         在 localhost     测试时，可以使用 Live Server（如 VS     Code 插件）或 ngrok 暴露 HTTPS 端口。

  
  

**【注意】不建议使用****js****的** **剪切板的****navigator.clipboard.readText()****！但****https****或****localhost****可正常写，****navigator.clipboard.writeText()****而其它非安全****http****域名则不行！**

  ![image.png](https://repo.in4tree.com/2026/01/14_1768434269123.png)

  

**注意：如果****navigator.clipboard.writeText()****出现错误****"Document is not focused."****，则关闭****F12****并刷新几次，应该就正常了。**

**注意：****JS****在非安全域名下****navigator.clipboard.writeText()****出错异常：****TypeError: Cannot read properties of undefined(reading 'writeText')** **（****https****或****localhost****可正常写）**

  
  

**[FIX#****在** **Chrome** **的** **DevTools** **控制台下执行** **navigator.clipboard** **返回** **undefined****，经查找资料发现是浏览器禁用了非安全域的****navigator.clipboard** **对象****]**

[https://www.cnblogs.com/hellxz/p/15192573.html](https://www.cnblogs.com/hellxz/p/15192573.html)

  
  
  
  
  

**【图片类型】远程图片****url****（容易导致****CORS****跨域问题！）**

如：[https://ibrainbook.com/img/logo.png](https://ibrainbook.com/img/logo.png)

  
  
  
  
  

**QQ****剪切板的****base64****图片**

  ![image.png](https://repo.in4tree.com/2026/01/14_1768434289352.png)

  

**文件夹复制的多个图片**

  ![image.png](https://repo.in4tree.com/2026/01/14_1768434304230.png)

  
  

**复制富文本（如****Word****文档中的超链接）**

  ![image.png](https://repo.in4tree.com/2026/01/14_1768434317900.png)

  
  
  

**【功能描述】**

包含缺省文字说明；能鼠标点选复制粘贴内容；

用户按Ctrl+v粘贴剪贴板中的内容到文本框，然后触发剪切板的粘贴事件，把剪切板内容进行HTML安全输入过滤，赋值为输入内容inputContent变量，然后显示到文本框；

JS验证inputContent变量是否合法：

1）如果该内容为图片网址URL链接（以http开头），则获取该URL链接的图片，执行图片处理过程；

2）如果该内容为base64图片，则获取该base64的图片，然后执行图片处理过程；

3）否则报错“剪贴板内容无效！只能是以http开头的图片网址URL链接，或者base64图片”

  
  

**图片处理过程：**

1）首先生成全路径文件名，格式为“全局路径常量/yyyy/mm/dd/时间戳.jpg”，然后把全路径文件名输出到HTML界面的文本框中；

2）然后调用PHP代码开始保存图片文件（如果目录不存在，则自动创建）  
  
  

**推荐使用剪切板的方法：用户按****Ctrl+V****，触发****paste****事件获取数据项：****event.clipboardData.items**

document.addEventListener("paste",function (event) {

    constitems = (event.clipboardData || event.originalEvent.clipboardData ||window.clipboardData).items; // 获取剪贴板中的数据项

   for (let item of items) {

       if (item.kind === "string") { // 检查是否是文本

           item.getAsString(function (text) {

                console.log("粘贴的文本内容:", text);

           });

       }

    }

});

**获取纯文本：** **event.****clipboardData.getData("text")**

document.addEventListener("paste",function (event) {

    consttext = const items = (event.clipboardData || event.originalEvent.clipboardData|| window.clipboardData).getData("text");

   console.log("粘贴的文本:", text);

});

  
  
  

**Uncaught Error: Call to undefined function curl_init()**

当JS#fetch调用PHP时，报错：Uncaught Error: Call to undefined function curl_init()。直接运行PHP则正常

原因：PHP7以上CURL安装方法更新了！导致localhost/test.php输出中没有curl相关内容！

解决：在apache配置文件中追加下面三行：

[https://www.youqizhuangbei.com/news/show-21028.html](https://www.youqizhuangbei.com/news/show-21028.html)

  ![image.png](https://repo.in4tree.com/2026/01/14_1768434374084.png)

  
  
  

**出错异常：无法保存图片！****PHP# imagejpeg()****返回****false****原因：目标路径不可写，或者目录不存在。**

  
  

**代码：****index.html**

  ![image.png](https://repo.in4tree.com/2026/01/14_1768434387061.png)

  ![image.png](https://repo.in4tree.com/2026/01/14_1768434398587.png)

  
  
  

**JS: uploadImage()**

  ![image.png](https://repo.in4tree.com/2026/01/14_1768434412202.png)

  

**PHP: upload.php**

![image.png](https://repo.in4tree.com/2026/01/14_1768434423519.png)

