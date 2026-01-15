  
![NodeJS：FIX：CORS跨域问题](https://repo.in4tree.com/2026/01/14_1768438438307.jpeg)  
  

**为什么会发生 CORS 错误？**

**不同端口导致跨域**

  

  

- - 前端运行在 http://localhost
    - 后端运行在 http://localhost:3000
    - 由于端口 3000 和 80（默认端口）不同，浏览器认为它们是不同的来源，触发      **CORS 限制**。

  

**Content-Type触发了 CORS 预检请求（Preflight）**

  

- - 你的 fetch() 请求包含 Content-Type:      application/json，这会导致浏览器发送 OPTIONS 预检请求。
    - 但后端 **没有允许 OPTIONS 请求**，导致请求被拒绝。

  
  

**（无效！）方法0：Chrome浏览器安装CORS扩展**

经常失效：

![NodeJS：FIX：CORS跨域问题](https://repo.in4tree.com/2026/01/14_1768438438685.jpeg)

  

**方法 1：在后端安装CORS NPM Package安装包：**

npminstall cors

  
  
**（无效！）后端代码加入：**

const cors =require("cors");  // ✅ 引入 cors 处理跨域

app.use(cors());  // ✅ 允许所有来源请求

![NodeJS：FIX：CORS跨域问题](https://repo.in4tree.com/2026/01/14_1768438438953.jpeg)

  

**（有效！）另一种：配置corsOptions，域名白名单**

[https://mufazmi.medium.com/solving-cors-issues-in-your-node-js-application-836506e63871](https://mufazmi.medium.com/solving-cors-issues-in-your-node-js-application-836506e63871)

const express = require('express');  
const cors = require('cors'); //Import the cors package  
  
const app = express();  
  
// Define the CORS options  
const corsOptions = {  
    credentials: true,  
    origin: ['http://localhost:3000', 'http://localhost:80'] //Whitelist the domains you want to allow  
};  

  
app.use(cors(corsOptions)); //Use the cors middleware with your options

  

**（有效！）Configuring CORS for Specific Origins**

[https://www.geeksforgeeks.org/how-to-deal-with-cors-error-in-express-node-js-project/](https://www.geeksforgeeks.org/how-to-deal-with-cors-error-in-express-node-js-project/)

const corsOptions = {  
    origin: 'http://example.com', // Allow only this domain  
    methods: 'GET,POST', // Allow only specific HTTP methods  
    allowedHeaders: 'Content-Type,Authorization' // Allow specific headers  
};  
  
app.use(cors(corsOptions));  
  
  

**CORS in Production Environment**

[https://www.geeksforgeeks.org/how-to-deal-with-cors-error-in-express-node-js-project/](https://www.geeksforgeeks.org/how-to-deal-with-cors-error-in-express-node-js-project/)

  
const corsOptions = {  
    origin: process.env.ALLOWED_ORIGIN || 'http://default-domain.com',  
    methods: 'GET,POST,PUT,DELETE',  
    credentials: true  
};

app.use(cors(corsOptions));// Use the cors middleware with your options

  
  

**（有效！）方法 2：手动设置 CORS 头**

如果不想使用 cors 库，也可以手动设置 CORS 头

app.use((req, res, next) => {

   res.header("Access-Control-Allow-Origin", "*");  // 允许所有来源

   res.header("Access-Control-Allow-Methods", "GET, POST,OPTIONS");  // 允许的方法

   res.header("Access-Control-Allow-Headers","Content-Type");  // 允许的头

   if (req.method === "OPTIONS") {

       return res.sendStatus(204);  // 预检请求直接返回 204

    }

   next();

});

![NodeJS：FIX：CORS跨域问题](https://repo.in4tree.com/2026/01/14_1768438439227.jpeg)

  

**（无效！）方法 3：前端 fetch 请求修改**

![NodeJS：FIX：CORS跨域问题](https://repo.in4tree.com/2026/01/14_1768438439527.png)  
  

**结论**

  

1. **推荐方法**：后端 **使用 cors 库** 解决跨域问题。
2. **手动 CORS 允许**：后端     res.header("Access-Control-Allow-Origin",     "*")。
3. **前端修改 fetch**：加上     mode: "cors"。
4. **清除浏览器缓存**

完成这些后，CORS 问题应该就能解决了！