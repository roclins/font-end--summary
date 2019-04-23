### HTTP协议

#### 一、HTTP协议是什么

HTTP的全称是超文本传输协议，是一种用于规定服务端和客户端之间传递数据的格式的一种传送协议。它是属于应用层上的协议，基于TCP/IP协议来传递数据。

#### 二、HTTP协议的使用

1. #### 报文组成

   请求报文由请求行、请求头、(空行)、请求体组成。

   请求行：请求方法+URL+HTTP协议版本，例如

   ```
   GET ./login.php HTTP/1.1
   ```

   请求头：

   ```
   Host: www.cnblogs.com 
   User-Agent: Mozilla/5.0 (Windows; U; Windows NT 5.0; zh-CN; rv:1.8.1) Gecko/20061010 Firefox/2.0  
   Accept: text/xml,application/xml,application/xhtml+xml,text/html;q=0.9,text/plain;q=0.8,image/png,*/*;q=0.5  
   Accept-Language: en-us,zh-cn;q=0.7,zh;q=0.3  
   Accept-Encoding: gzip,deflate  
   Accept-Charset: gb2312,utf-8;q=0.7,*;q=0.7  
   Keep-Alive: 300  
   Proxy-Connection: keep-alive  
   Cookie: ASP.NET_SessionId=ey5drq45lsomio55hoydzc45
   Cache-Control: max-age=0
   ```

   请求体

2. 响应报文

   响应报文：响应行+响应头+响应体

   响应行由HTTP协议版本+状态码+状态码解释短语组成

   ```
   HTTP/1.1 200 OK
   ```

   响应头，例如

   ```
   Date: Tue, 12 Jul 2016 21:36:12 GMT
   Content-Length: 563
   Content-Type: text/html
   ```

   响应体：可以是一个HTML，也可以是一串数据

#### 2.请求方法

1. **GET**：获取资源，同时也指定了服务器处理请求之后响应的内容 ，例如：

   ```
   https://www.baidu.com/s?ie=UTF-8&wd=aaa
   ```

2. **POST**：**传输实体主体** 

3. **PUT：传输文件** 

   文件内容包含在请求报文的实体中，然后请求保存到URL指定的服务器位置。 

4. **DELETE：删除文件** 

   DELETE方法用来删除文件，是与PUT相反的方法。

5. **HEAD：获得报文首部** 

   HEAD方法类似GET方法，但是不同的是HEAD方法不要求返回数据，只返回一个头。用于确认资源是否存在

6. **OPTIONS：询问支持的方法** 

   预检请求。它用于获取当前URL所支持的方法。 服务端返回的响应报文中会有一个“Allow”的头，值是所支持的方法，如“GET, POST”。 

#### 3.HTTP响应状态码

|      |     类别     |         原因短语         |
| :--: | :----------: | :----------------------: |
| 1xx  |  信息状态码  |    接收的请求正在处理    |
| 2xx  |  成功状态码  |       请求正常处理       |
| 3xx  | 重定向状态码 | 要完成请求需要进一步操作 |
| 4xx  |  客户端错误  |     一般是有语法错误     |
| 5xx  |  服务端错误  |    服务端处理请求出错    |

1. 200 OK

   代表请求被正常处理了，也是我们最希望见到的

2. 201 created

   表示请求已被处理，上传的资源已成功被创建，常用与PUT请求

3. 204 not content

   请求响应报文中不含实体部分，浏览器不需要离开当前页面，不需要刷新页面，例如用户短时间连续刷新网页

4. 205 reset content

   响应不包含实体部分，提示浏览器重置页面，例如刷新表单，重新渲染UI等

5. 301 Moved Permanently

   代表永久性定向。指示所请求的资源已明确移动到`Location`标题给定的URL 。  

6. 302：Found

   临时重定向。指示所请求的资源已暂时移动到由`Location`标题给定的 URL 。 

7. 303 See Other

   通常作为 [`PUT`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/PUT) 或 [`POST`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/POST) 操作的返回结果，它表示重定向链接指向的不是新上传的资源，而是另外一个页面，比如消息确认页面或上传进度页面。而请求重定向页面的方法要总是使用 [`GET`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/GET)。 

8. 304 not modified

   重定向到缓存资源。

9. 307 Temporary Redirect

   临时重定向。307能够保证原始请求中的方法和实体，在重定向请求中不被改变。因为有些老旧的浏览器对302的处理会在重定向请求中，把方法改为GET

10. 400 Bad Request 

  400 表示报文中存在语法错误，需要修改后再发送

11. 401 Unauthorized

    请求未经授权，表示发送的请求需要有通过HTTP认证的认证信息。 这个状态代码必须和WWW-Authenticate 报头域一起使用。WWW-Authenticate: Basic realm="Access to the staging site"

12. 403 Forbidden

    请求访问的资源被拒绝了，没有获得服务器的访问权限，IP被禁止等

13. 404 Not Found

    资源不存在，例如输入了错误的URL

14. 500 Internal Server Error

    服务端出错，可能有BUG。

15. 503 Server Unavailable

    服务器当前不能处理客户端的请求，一段时间后可能恢复正常。

#### 4.HTTP头

1. 通用头部（上面几个是常用的）

   |     通用字段      |             作用             |              值               |
   | :---------------: | :--------------------------: | :---------------------------: |
   |   Cache-Control   |        控制缓存的行为        |    max-age=60（缓存 60s）     |
   |    Connection     | 浏览器想要优先使用的连接类型 |      keep-alive、closed       |
   |       Date        |         创建报文时间         | Tue, 12 Jul 2016 21:36:12 GMT |
   |      Pragma       |           报文指令           |                               |
   |        Via        |      代理服务器相关信息      |                               |
   | Transfer-Encoding |         传输编码方式         |                               |
   |      Upgrade      |      要求客户端升级协议      |                               |
   |      Warning      |     在内容中可能存在错误     |                               |

2. 请求头部

   |      请求头部       |                             作用                             |                             值                             |
   | :-----------------: | :----------------------------------------------------------: | :--------------------------------------------------------: |
   |       Accept        |              能正确接收的媒体类型 （文件类型）               |                 text/html,text/javascript                  |
   |   Accept-Charset    |                      能正确接收的字符集                      |                           utf-8                            |
   |   Accept-Encoding   |                   能正确接收的编码格式列表                   |                            gzip                            |
   |   Accept-Language   |                     能正确接收的语言列表                     |                        en-us,zh-cn                         |
   |        Host         |                        请求服务端域名                        |                       www.baidu.com                        |
   |   **User-Agent**    |                          客户端信息                          | 浏览器信息，系统信息，可以根据它返回一个PC站点或者移动站点 |
   |  WWW-Authenticate   |                           认证信息                           |         Basic realm="（用户名：密码）的base64编码"         |
   |       Referer       | 首部包含了当前请求页面的来源页面的地址，即表示当前页面是通过此来源页面里的链接进入的。 |                                                            |
   |       Cookies       |                                                              |                                                            |
   | Last-Modified-Since |   用于确认资源新鲜度，值为上次服务端发送过的Last-Modified    |                                                            |
   |    If-None-Match    |                     用于确认资源是否更改                     |                                                            |

   user-agent：游览器的信息，可以根据这个，返回对应的网页，例如，手机请求百度，和网页请求的百度，呈现出的页面的不同，就是服务端user-agent不同，返回的网页也不同

3. 响应头部

   |   响应头部    |            作用            |  值  |
   | :-----------: | :------------------------: | :--: |
   |    Server     |         服务器名字         |      |
   |      Age      | 资源在代理缓存中存在的时间 |      |
   |   Location    |   客户端重定向到某个 URL   |      |
   |  Set-cookies  |                            |      |
   |    Expeirs    |      缓存资源过期时间      |      |
   | Last-Modified |      资源上次更改时间      |      |
   |     ETag      |      资源的唯一标识码      |      |
   |               |                            |      |

4. 实体头部

   |     实体头部     |        作用        |          值           |
   | :--------------: | :----------------: | :-------------------: |
   |      Allow       | 资源的正确请求方式 | 跟方法options配合使用 |
   | Content-Encoding |   内容的编码格式   |         gzip          |
   | Content-Language |   内容使用的语言   |                       |
   | Content-Location | 返回数据的备用地址 |                       |
   |   Content-Type   |   内容的媒体类型   |       text/html       |
   |                  |                    |                       |
   |                  |                    |                       |
   |                  |                    |                       |

#### 5.HTTPS

HTTPS 就是在浏览器传包给服务端时，先把包经过了一个加密服务器进行加密，再传输，它不是一个新的协议 .

HTTPS 还是通过了 HTTP 来传输信息，但是信息通过 TLS 协议进行了加密。

TLS 协议位于传输层之上，应用层之下。首次进行 TLS 协议传输需要两个 RTT ，接下来可以通过 Session Resumption 减少到一个 RTT。

在 TLS 中使用了两种加密技术，分别为：对称加密和非对称加密。

协议为HTTP，端口为80 ，协议为HTTPS： 端口为443

#### 6.HTTP1.1

现在的HTTP版本支持管道机制，可以同时请求和响应多个请求，大大提高了效率。 

现在使用的版本当中是默认持久连接的，也就是多次HTTP请求使用一个TCP连接。 

#### 7.注意

##### 1.get 和 post 

get请求一般只是向[服务器](https://www.baidu.com/s?wd=%E6%9C%8D%E5%8A%A1%E5%99%A8&tn=24004469_oem_dg&rsv_dl=gh_pl_sl_csd)请求数据（这是约定而成的），为了更快完成操作，会在本地缓存数据以便将来再次访问；

而post请求一般用于update/submit更新提交数据，所以此时缓存数据就显得很蠢了；

所以才有了：get会缓存数据，而post不缓存数据 的说法。

##### 2.浏览器发起一个请求全过程

1. 用户在浏览器中输入URL地址
2. 浏览器解析用户输入的URL地址 => 域名 + 端口
3. 浏览器先会检查自己的本地缓存中有没有这个域名 => IP
4. 如果没有，则会发起一个DNS系统调用 =>IP
   - 先检查操作系统中的DNS缓存（维护一张域名与IP地址的对应表） 
   - 如果没有，则搜索操作系统中的hosts文件
   - 如果还没有，则会对DNS服务器发起一个系统调用（本地没有，网上查）
5. 浏览器会通过一个本地的随机端口建立一个与服务器指定端口之间的连接通道
6. 浏览器会将客户端的一些信息打上一个“包”
7. 将这个包通过这个连接通道发送给服务端

##### 3.浏览器解析网址IP全过程（与第二点互补，较为全面）

1. 浏览器搜索自己的DNS缓存（维护一张域名与IP地址的对应表）

2. 若没有，则搜索操作系统中的DNS缓存（维护一张域名与IP地址的对应表）

3. 若没有，则搜索操作系统的hosts文件（Windows环境下，维护一张域名与IP地址的对应表，位置一般在 C:\Windows\System32\drivers\etc\hosts）

4. 若没有，则操作系统将域名发送至 本地域名服务器- -（递归查询方式），本地域名服务器 查询自己的DNS缓存，查找成功则返回结果，否则，（以下是迭代查询方式）

   4.1 本地域名服务器 向根域名服务器（其虽然没有每个域名的具体信息，但存储了负责每个域，如com、net、org等的解析的顶级域名服务器的地址）发起请求，此处，根域名服务器返回com域的顶级域名服务器的地址

   4.2 本地域名服务器 向com域的顶级域名服务器发起请求，返回baidu.com权限域名服务器（权限域名服务器，用来保存该区中的所有主机域名到IP地址的映射）地址

   4.3 本地域名服务器 向baidu.com权限域名服务器发起请求，得到www.baidu.com的IP地址

5. 本地域名服务器 将得到的IP地址返回给操作系统，同时自己也将IP地址缓存起来

6. 操作系统将 IP 地址返回给浏览器，同时自己也将IP地址缓存起来

7. 至此，浏览器已经得到了域名对应的IP地址 





