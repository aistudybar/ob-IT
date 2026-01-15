
---
目录：
上一页：
下一页：
关键词：
相关链接：

---


**1. 过滤 XSS 攻击XSS攻击通常通过注入恶意脚本来实现。为了防止 XSS 攻击，你可以对用户输入的内容进行转义。**

·  转义 \<, >，防止插入 \<script> 标签。

·  转义 " 和 '，防止属性注入攻击（如）。

·  去除 script, alert 等关键字，避免 JS 代码执行。

```js
function escapeHTML(str) {  
    return str.replace(/&/g, '&')  
              .replace(/</g, '<')  
              .replace(/>/g, '>')  
              .replace(/"/g, '"')  
              .replace(/'/g, ''');  
}  
const userInput = '<script>alert("XSS")</script>';  
const safeInput = escapeHTML(userInput);  
console.log(safeInput); // 输出: <script>alert("XSS")</script>  
```


**2. 过滤 SQL 注入SQL注入通常通过用户输入中的特殊字符（如单引号 '、分号 ; 等）来实现。为了防止 SQL 注入，你应该对用户输入进行转义或使用参数化查询。**

```js
function escapeSQL(str) {  
    return str.replace(/'/g, "''")  
              .replace(/--/g, '')  
              .replace(/;/g, '');  
}  
const userInput = "';  
DROP TABLE users; --";  
const safeInput = escapeSQL(userInput);  
console.log(safeInput); // 输出: ''; DROP TABLE users;    
```


**3. 使用正则表达式进行输入验证你可以使用正则表达式来验证用户输入是否符合预期的格式。**

```js
function validateInput(input) {  
    // 只允许字母、数字和下划线  
    const regex = /^[a-zA-Z0-9_]+$/;  
    return regex.test(input);  
}  
const userInput = 'user123';  
if (validateInput(userInput)) {  
    console.log('输入有效');  
} else {  
    console.log('输入无效');  
}     
```


**4. 使用 DOM Purify 进行 XSS 过滤如果你需要处理富文本输入（如 HTML），可以使用** [DOMPurify](https://github.com/cure53/DOMPurify"%20\t%20"_blank) **这样的库来过滤潜在的 XSS 攻击。**

```js
<script src="https://cdnjs.cloudflare.com/ajax/libs/dompurify/2.3.6/purify.min.js"></script><script>  
    const userInput = '<script>alert("XSS")</script><p>Hello</p>';  
    const cleanInput = DOMPurify.sanitize(userInput);  
    console.log(cleanInput); // 输出: <p>Hello</p>  
</script>      
```


**5. （避免单独使用！）使用隐藏的 div 或文本框内置 HTML 解析机制进行输入过滤转义危险内容**

创建隐藏的 div 或文本框并读取其内容并不是一种安全的方式，因为这种方式并不能有效防止 XSS 或 SQL 注入攻击。相反，你应该直接在输入时对用户输入进行验证和过滤。  
**示例代码**

[https://grok.com/chat/cf49bf39-d93e-4abf-8fee-093af5c590ca](https://grok.com/chat/cf49bf39-d93e-4abf-8fee-093af5c590ca)

// 创建一个安全的输入过滤器

```js
   function createInputSanitizer() {  
    // 创建一个隐藏的div 用于检测  
    const hiddenDiv =document.createElement('div');  
    hiddenDiv.style.display ='none';  
   document.body.appendChild(hiddenDiv);  
   // 定义常见的危险字符和模式  
   const dangerousPatterns= [  
       /<script\b[^<]*(?![？？？JS过滤HTML输入](https://repo.in4tree.com/2026/01/14_1768438536617.gif)?!<\/script>)<[^<]*)*<\/script>/gi,// XSS: script标签  
       /on\w+="[^"]*"/gi,                                    // XSS: 事件属性

       /javascript:/gi,                                      // XSS:javascript协议

       /['";--]/g,                                          //SQL注入: 单引号、双引号、分号、注释

       /\b(union|select|insert|delete|update|drop|alter)\b/gi // SQL注入: 常见关键字

   ];

   // 过滤函数

   function sanitizeInput(input) {

       // 首先将输入放入隐藏div

       hiddenDiv.innerHTML = input;

       // 获取处理后的文本内容（浏览器会自动转义一些HTML）

       let sanitized = hiddenDiv.textContent || hiddenDiv.innerText;

       // 执行额外的正则过滤

       dangerousPatterns.forEach(pattern => {

           sanitized = sanitized.replace(pattern, '');

       });

       // 清理特殊字符

       sanitized = sanitized

           .replace(/[<>&'"]/g, match => { // 转义HTML字符

                return {

                    '<': '<',

                    '>': '>',

                    '&': '&',

                    '"': '"',

                    "'": '''

                }[match];

            })

           .trim();

       return sanitized;

    }

   // 示例用法

   function validateAndFilter(input) {

       const cleanedInput = sanitizeInput(input);

       console.log('原始输入:', input);

       console.log('过滤后:', cleanedInput);

       return cleanedInput;

    }

   // 测试用例

   const testCases = [

       "<script>alert('xss')</script>",

       "SELECT * FROM users WHERE id = '1' OR '1'='1';--",

       "onclick=\"alert('hacked')\"",

        "Normal text with<b>bold</b>",

       "javascript:alert('test')"

   ];

   // 运行测试

   testCases.forEach(test => validateAndFilter(test));

   // 清理隐藏div

   return {

       sanitize: sanitizeInput,

       cleanup: () => document.body.removeChild(hiddenDiv)

   };

}

// 使用示例

const sanitizer = createInputSanitizer();

// 在实际应用中这样使用

const userInput ="<script>alert('xss')</script> UNION SELECT password FROMusers";

const safeInput =sanitizer.sanitize(userInput);

console.log(safeInput);

// 当不再需要时清理

// sanitizer.cleanup(); 
```


