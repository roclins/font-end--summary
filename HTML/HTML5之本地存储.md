### 本地存储

HTML5中多了localStorage对象、sessionStorage对象来支持本地存储。

以前，一般是使用Cookie来进行本地存储。Cookie 是服务器 存储数据到 浏览器 的一种技术，用于跟踪客户状态。比如证明客户身份： 是否是第一次访问，是否已经登录等。

cookie流程:
    1.客户端首次访问服务器，服务端会现在客户端存留该客户的相关信息的cookie；
    2.以后客户每次访问服务器时，都会在HTTP请求中包含cookie数据，服务器解析cookie，就能得到客户的信息；

##### cookies，sessionStorage和localStorage的区别

共同点：都是保存在浏览器端，且是同源的。

sessionStorage 是HTML5新增的一个会话存储对象，用于临时保存同一窗口(或标签页)的数据，在关闭窗口或标签页之后将会删除这些数据。 

|                                    |                       cookie                       | localStorage | sessionStorage |
| :--------------------------------: | :------------------------------------------------: | :----------: | :------------: |
|             由谁初始化             | 客户端或者服务端，，服务端可以使用Set-Cookie请求头 |    客户端    |     客户端     |
|              过期时间              |                      手动设置                      |   永不过期   | 当前页面关闭时 |
|   在当前浏览器会话中是否保持不变   |              取决于是否设置了过期时间              |      是      |       否       |
| 是否随着每次 HTTP 请求发送给服务器 |   是，cookie会通过Cookie请求头，自动发送给服务端   |      否      |       否       |
|                容量                |                        4kb                         |      5M      |       5M       |
|              访问权限              |                      任意窗口                      |   任意窗口   |    当前窗口    |

区别：

1. cookies是为了标识用户身份而存储在用户本地终端上的数据，始终在同源http请求中携带，即cookies在浏览器和服务器间来回传递，而sessionStorage和localStorage不会自动把数据发给服务器，仅在本地保存。
2. 存储大小的限制不同。cookie保存的数据很小，不能超过4k，而sessionStorage和localStorage保存的数据大，可达到5M。
3. 数据的有效期不同。cookie在设置的cookie过期时间之前一直有效，即使窗口或者浏览器关闭。sessionStorage仅在浏览器窗口关闭之前有效。localStorage始终有效，窗口和浏览器关闭也一直保存，用作长久数据保存。
4. 作用域不同。cookie在所有的同源窗口都是共享；sessionStorage不在不同的浏览器共享，即使同一页面；localStorage在所有同源窗口都是共享

#### localeStorage的使用

```javascript
//lcoalStorage是一个对象，在window中
<script>
    if(window.localStorage){
        console.log("浏览器支持localStorage");
        let localStorage = window.localStorage;
        //=======================================
        //增：
        //1.
        localStorage['name1'] = "Roclin" ;
        //2.
        lcoalStorage.name2 = "Roclin";
        //3.
        localStorage.setItem("name3","Roclin");
        
        //=======================================
        //删：
        //1.删键值对
        localStorage.removeItem("name1");
        //2.删全部
        lcoalStorage.clear()
        
        //======================================
        //改：
        localStorage.name2 = "roclin";
        
        //======================================
        //查：
        //1.
        console.log(localStorage.a);
        //2.
        localStorage.getItem("name3");
    } 
</script>			
```



https://www.cnblogs.com/st-leslie/p/5617130.html

