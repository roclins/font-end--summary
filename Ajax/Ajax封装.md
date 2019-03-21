```javascript
/**
 * 发送一个 AJAX 请求
 * @param  {String}   method 请求方法
 * @param  {String}   url    请求地址
 * @param  {Object}   data 请求参数
 * @param  {Function} callback   请求完成过后需要做的事情（委托/回调）
 */

	function ajax(url,methods,data,callback) {
		//将方法转换为大写
		methods = methods.toUpperCase();

		// 对象形式的参数转换为 urlencoded 格式
		let params = [];
		for (let key in data) {
			params.push(key + "=" + data[key]);
		}
		let queryString = params.join('&');

		let xhr = window.XMLHttpRequest()?new XMLHttpRequest(): ActiveXObject('Microsoft.XMLHTTP');

		//如果是GET请求，设置URL
		if (methods === 'GET') {
			url = url + '?' + queryString;
		};
		xhr.open(methods,url);
		
		//如果是POST请求，设置请求体
		let sendData = null;
		if (methods === 'POST') {
			sendData = queryString;
			xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded')
		};
		xhr.send(sendData);
		
		//绑定事件，处理响应
		xhr.addEventListener('readystatechange',fucntion(){
			if(this.readyState !== 4) {
				return
			}
			callback(this.response);
		})
        
        
        ajax('./a.php','POST',{ id:1,name:'roclin' },function(data){
            console.log(data)
        })
```

