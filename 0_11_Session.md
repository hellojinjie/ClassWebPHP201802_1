## PHP 会话控制
**思考** 为留言板增加删除留言功能，只有管理员才能删除。当管理员登录之后，怎么识别管理员的身份？

### Cookies
一种在远程客户端（浏览器）存储数据用来跟踪和识别用户的机制。

 1. 用户访问网站；
 2. 网站向浏览器写入 cookie；
 3. 用户带上前面的cookie，第二次访问网站
 4. 网站读取到cookie

#### HTTP 协议角度
* 如何向浏览器写入 cookie
	* 通过 response header 发送 cookie，Set-Cookie: username=JinJie
* 如何向网站发送 cookie
	* 通过 request header 发送 cookie，Cookie: username=JinJie
#### PHP 代码
* 如何写 cookie
	* setcookie(name, value, expire, path, domain, secure, httponly);
* 如何在代码里读取 cookie
	* $_COOKIE['cookiename']

#### 过期时间 
* **会话 cookie** 	新建cookie默认是会话cookie，有效期直到浏览器关闭。（有些浏览器有会话自动恢复的功能）
* **持久 cookie** 指定一个特定的过期时间（expire），在过期时间到来之前，会一直存在并有效。

#### 有效路径
Cookie 在服务端的有效路径 ，默认为当前路径
url 的组成  schema://domain/path/filename?querystring

#### 有效域名
Cookie 的有效域名，默认为当前域名

#### Secure
值为 1或0，如果是1，则只能通过https是设置和访问cookie

#### httponly
不能通过 javascript 来读写cookie

### 练习1
1. 向浏览器写入 cookie username=123
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTYwNjQwNzg3MV19
-->