**  
原因：navigator.clipboard或剪切板库clipboard-polyfill requires a secure origin（https），所以除**[http://localhost](http://localhost/"%20\t%20"_blank)**以外，都不支持！NAS服务器需要有https域名才行。**

Clipboardfeature is available only in secure contexts (HTTPS), in some or all supportingbrowsers. You need change protocol to https (SSL)

![NodeJS：ERR：Cannot read properties of undefined （reading 'readText'）](https://repo.in4tree.com/2026/01/14_1768463168833.jpeg)

  

**不使用 navigator.clipboard 的情况下读取剪贴板解决：手动按 Ctrl+ V / Cmd + V 粘贴（缺点是无法自动获取剪切板内容）**

<input type="text"id="textBox" placeholder="请粘贴内容">

<script>

document.addEventListener("**paste**",function(event) {

   let pasteData = **event.clipboardData** || window.clipboardData;  // 获取剪贴板数据

   let pastedText = pasteData.**getData**("text");  // 读取文本内容

   event.target.value = pastedText; // 显示在输入框

   event.preventDefault();  // 阻止默认粘贴行为

});

</script>