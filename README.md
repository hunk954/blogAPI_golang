## 模仿Github，设计一个博客网站的API
### 17级服务计算 17308154 王俊焕
### 一、REST API是什么
REST是Transfer（表现层状态转移）的缩写，它是由罗伊·菲尔丁（Roy Fielding）提出的，是用来描述创建HTTP API的标准方法的，他发现这四种常用的行为（查看（view），创建（create），编辑（edit）和删除（delete））都可以直接映射到HTTP 中已实现的GET,POST,PUT和DELETE方法。
### 二、架构
所有API访问都是通过HTTPS进行，并且可以通过访问`https://api.blogWorld.com`。所有数据都以JSON的形式发送和接受。所有的时间戳都以ISO 8601格式返回： 
```YYYY-MM-DDTHH:MM:SSZ```
### 三、登录操作（认证方式）
`curl -u 'username' https://api.blogWorld.com`
### 四、
### 参考资料
- [Github API v3 overview](https://developer.github.com/v3/)
