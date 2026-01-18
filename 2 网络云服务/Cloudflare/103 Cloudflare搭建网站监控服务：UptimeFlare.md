
---
目录：
上一页：
下一页：
关键词：
相关链接：

---

# 特点

UptimeFlare 是一个更先进、无服务器且免费的正常运行时间监控和状态页面解决方案，由 Cloudflare Workers 提供支持，并配有用户友好的界面

![image.png](https://repo.in4tree.com/2026/01/17_1768717303011.png)

![image.png](https://repo.in4tree.com/2026/01/17_1768717417091.png)

- 监控能力
    - 每隔 1 分钟最多进行 50 次检查
    - 来自全球[310](https://www.freedidi.com/?golink=aHR0cHM6Ly93d3cuY2xvdWRmbGFyZS5jb20vbmV0d29yay8=&nonce=7cd34930e1)多个城市的地理位置特定检查
    - 支持 HTTP/HTTPS/TCP 端口监控
    - 最多可跟踪 90 天的正常运行时间历史记录和正常运行时间百分比
    - 可自定义的 HTTP(s) 请求方法、标头和正文
    - HTTP(s) 的自定义状态码和关键字检查
    - 支持[100 多个通知渠道的停机通知](https://www.freedidi.com/?golink=aHR0cHM6Ly9naXRodWIuY29tL2Nhcm9uYy9hcHByaXNlL3dpa2k=&nonce=7cd34930e1)
    - 可定制的 Webhook

- 状态页面
    - 适用于所有类型显示器的交互式 ping（响应时间）图表
    - 计划维护提醒和事件历史记录页面
    - 响应式用户界面，可适应您的系统主题
    - 可自定义状态页面
    - 使用 CNAME 记录将您自己的域名添加到您的域名记录中。
    - 可选密码验证（私密状态页面）
    - 用于获取实时状态数据的 JSON API


# **UptimeFlare：【[链接直达](https://www.freedidi.com/?golink=aHR0cHM6Ly9naXRodWIuY29tL2x5Yzg1MDMvVXB0aW1lRmxhcmU=&nonce=7cd34930e1)】**

# 在 Cloudflare 上设置您自己的 Uptimeflare：

1. 使用模板在[https://dash.cloudflare.com/profile/api-tokens](https://www.freedidi.com/?golink=aHR0cHM6Ly9kYXNoLmNsb3VkZmxhcmUuY29tL3Byb2ZpbGUvYXBpLXRva2Vucw==&nonce=7cd34930e1)创建 API 令牌。
   `Edit Cloudflare Workers`
   ![](https://www.freedidi.com/wp-content/uploads/2025/10/49dba68c9c20251031231209.gif)
2. 点击此处，在您的帐户中创建[此仓库](https://www.freedidi.com/?golink=aHR0cHM6Ly9naXRodWIuY29tL2x5Yzg1MDMvVXB0aW1lRmxhcmU=&nonce=7cd34930e1)的副本`Use this template`。如果您不希望其他人看到您的监控定义，您可以选择将其设置为私有。（您可以直接在其中包含令牌）。
   ![](https://www.freedidi.com/wp-content/uploads/2025/10/274a01ad7a20251031231112-scaled.gif)
3. 在 中设置您的 Cloudflare API Token `Settings - Secrets and variables - Actions`，设置一个密钥，其键为`CLOUDFLARE_API_TOKEN`，值为您在步骤 1 中获得的令牌。您的令牌将由 GitHub 安全地存储。
   ![](https://www.freedidi.com/wp-content/uploads/2025/10/068ae4052320251031231234.gif)
4. 编辑该`uptime.config.ts`文件（位于您自己的存储库的根目录下）以定义您的监视器并自定义您的状态页面，有关更详细的说明，请参阅[文档。](https://www.freedidi.com/?golink=aHR0cHM6Ly9naXRodWIuY29tL2x5Yzg1MDMvVXB0aW1lRmxhcmUvd2lraS9Db25maWd1cmF0aW9u&nonce=7cd34930e1)编辑完成后，导航至此处`Actions`查看部署进度。管道成功后，您应该会在 Cloudflare 帐户的此处看到“已成功部署”的状态页面`Workers & Pages`。
   ![](https://www.freedidi.com/wp-content/uploads/2025/10/09dd8c266220251031231337-scaled.png)
5. 如需稍后更新或修改配置，只需`uptime.config.ts`再次编辑即可。如果配置正确，管道会自动获取您的更改并将其应用到 Cloudflare Pages。


# 【参考】

[Cloudflare 免费用到爽！Workers/Pages 搭建无限图床、个人导航站、博客等全搞定！ | 零度解说](https://www.youtube.com/watch?v=VrYfC85Bj0o)

UptimeFlare 搭建网站监控服务：[https://www.freedidi.com/21369.html](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbml1Z3l3VUxyVDJCZDB1UlFwRk5yeF8wYm1zUXxBQ3Jtc0tuTWYyYWpBMTFnYXdpMk5WU0g0UVJfdmE4OVhBUTJJNlJ0cWJDNWZiajRSaDhhQnNHdUZXdnZoZnhENVV6bGwxM2hRS0JCbmJ2aWVtcGZoVlVJeHBSTU9SZURLMDFjZ0FMdVRhMTZMTl9sSkw1eXZqdw&q=https%3A%2F%2Fwww.freedidi.com%2F21369.html&v=VrYfC85Bj0o)
