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

**思考** 并没有相关的删除cookie的api，如何删除一个  cookie
1. expire 为0 或空：会话 cookie
2. 大于当前时间的 unix timestamp：持久 cookie
3. 小于或等于当前时间：删除 cookie（已过期的 cookie毫无意义）

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
1. 向浏览器写入 cookie username=123，
	- 尝试不同的参数值；
	- 通过浏览器的调试功能查看 cookie 的传递和存储 
2. 读取 $_COOKIE['username']

### Cookie 有哪些不足的地方
1. 所有的数据都存储在客户端，数据容易被篡改；
2. 大量的数据通过 cookie 存储占用客户磁盘空间；
3. 每次访问网站都需要带上cookie，如果数据大了，就会占用很大的网络空间；
	- 为什么很多的网站，静态资源都是使用单独的域名？    

如何解决这些问题？将数存储在服务器上。

### Session


<!--stackedit_data:
eyJoaXN0b3J5IjpbNTU5ODMwMzMzXX0=
-->