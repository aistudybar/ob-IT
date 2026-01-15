**AI提示词**

php编写一个wordpress plugin，该插件接收外部php fetch()传递的json数据（其中定义了帖子标题、内容文本、发帖者）。要求有发帖权限，比如为wordpress管理员  
  
  

**插件代码文件**

  
![！WordPress插件开发：远程发布帖子DEMO（external-json-post-creator）](https://repo.in4tree.com/2026/01/14_1768437836970.jpeg)  
  

**WordPress后台查看修改插件代码**

![！WordPress插件开发：远程发布帖子DEMO（external-json-post-creator）](https://repo.in4tree.com/2026/01/14_1768437837355.jpeg)  
  
  
  

**// 注册 REST API 端点**

add_action('rest_api_init', function () {  
    ///激活插件后，访问任意一个网页路由时，插件才注册（即log中显示'rest_api_init triggered'）  
    error_log('rest_api_init triggered'); ///写入日志  
    register_rest_route('external-json/v1', '/create-post', array(  
        'methods' => 'POST',  
        'callback' => 'handle_json_post_creation',  
        'permission_callback' => 'restrict_to_admins'  
    ));  
});  
  
  

**// 在WordPress后台激活插件时，显示“External JSON Post Creator 已加载”**

add_action('admin_notices', function() {  
    echo '<div class="notice notice-success"><p>External JSON Post Creator 已加载</p></div>';  
});  
  
  
  
  

**{"code":"rest_forbidden","message":"Sorry, you are not allowed to do that.","data":{"status":401}}**

**The application password feature requires HTTPS, which is not enabled on this site.**

///禁用 HTTPS 检查  
///后台=》User=》Profile：If this is a development website, you can set the environment type accordingly to enable application passwords.  
define('WP_ENVIRONMENT_TYPE', 'local');  
![！WordPress插件开发：远程发布帖子DEMO（external-json-post-creator）](https://repo.in4tree.com/2026/01/14_1768437837663.jpeg)  
  
![！WordPress插件开发：远程发布帖子DEMO（external-json-post-creator）](https://repo.in4tree.com/2026/01/14_1768437837898.jpeg)  

**外部PHP代码**

  
![！WordPress插件开发：远程发布帖子DEMO（external-json-post-creator）](https://repo.in4tree.com/2026/01/14_1768437838155.jpeg)