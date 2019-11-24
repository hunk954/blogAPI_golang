## 模仿Github，设计一个博客网站的API
### 17级服务计算 17308154 王俊焕
### 一、REST API是什么
REST是Transfer（表现层状态转移）的缩写，它是由罗伊·菲尔丁（Roy Fielding）提出的，是用来描述创建HTTP API的标准方法的，他发现这四种常用的行为（查看（view），创建（create），编辑（edit）和删除（delete））都可以直接映射到HTTP 中已实现的GET,POST,PUT和DELETE方法。
### 二、架构

- 访问格式

  所有API访问都是通过HTTPS进行，并且可以通过访问`https://api.blogWorld.com`。所有数据都以JSON的形式发送和接受。所有的时间戳都以ISO 8601格式返回： 
  ```YYYY-MM-DDTHH:MM:SSZ```

- HTTP动词

  与REST API呼应，将增(update)删(delete)改(edit)查(view)的操作映射到HTTP中已实现的GET、POST、PUT、DELETE方法中。
|动词|描述|
|:-:|:-:|
|GET|用于检索资源，对应查|
|POST|用于创建资源，对应增|
|PUT|用于替换资源或集合。对于`PUT`没有`body`属性的请求，需确保`Content-Length`标头设置为零，对应改|
|DELETE|用于删除资源，对应删|


- 响应状态码（详细内容见[HTTP Status Code](https://www.w3.org/Protocols/HTTP/HTRESP.html)）
|状态码|状态|
|-|-|
|2XX|表示请求成功|
|3XX|表示重定向|
|4XX|请求错误|

- 访问根目录以获得所有API使用方法
	```shell
	curl https://api.blogWorld.com
	```

### 三、登录操作（认证方式）
- 基本方式
    - 用户在参数中输入名称，但不输入密码。回车后终端再次让用户输入密码，此时密码不回显
        `curl -u username https://api.blogWorld.com`
    - 用户同时输入用户名和密码
    	`curl -u username:password https://api.blogWorld.com`
- 登录成功（返回202 Accepted）
```shell
curl -i https://api.blogWorld.com -u valid_name:valid_password
HTTP / 1.1 202 Accepted
{
	"message":"login successed"
	"user":valid_name
}
```

- 登录限制失败（例如使用无效的凭据进行身份验证将返回`401 Unauthorized`）
```shell
curl -i https://api.blogWorld.com -u invalid_name:invalid_password
HTTP / 1.1 401 Unauthorized
{
	"message":"The user does not exist or the password is wrong"
	"documentation_url":"https://api.blogWorld.com"
}
```
- 若在短时间内检测到多个具有无效凭据的请求后，API会临时拒绝该用户的所有身份验证尝试（包括具有有效凭据的请求）：`403 Forbidden`
```shell
curl -i https://api.blogWorld.com -u valid_username:valid_password
HTTP / 1.1 403 Forbidden
{
	"message":"Frequent login requests"
	"documentation_url":"https://api.blogWorld.com"
}
```
### 四、GET请求获得博客内容

- 摘要表示：`GET /user/articles/article1/repo`
- 指定页面表示： `GET user/articles/article1?page=2&per_page=100`
- 详细表示：`GET /user/articles/article1/detail`
- 若上述请求成功则会产生并返回一个资源，包含博客的基本内容
```shell
HTTP / 1.1 200 OK
{
	"username":valid_username
	"total_count":20
	"articles":[
		"id":02
		"headline":"title"
		"author":"author's name"
		"url":"url"
		"private":false
		"description":"detail.."
		"content":"..."
		"encoding":"UTF-8"
        ...
	]
}
```
### 五、POST请求创建新博客
### 六、PUT请求更新博客内容
### 七、DELETE删除博客

### 参考资料
- [Github API v3 overview](https://developer.github.com/v3/)
