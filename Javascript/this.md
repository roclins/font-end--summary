### this

总结：this指向的是`调用`它的那个`对象`。this 的情况可以分为以下几种：

- 普通函数的`this`
- `obj.foo()`中
- `new` + 构造函数
- call、apply、bind等
- 箭头函数

### 普通函数的this

对于普通函数，无论它放在什么地方，this一定指向的是window

### obj.foo()

谁调用foo，foo中的this就指向谁

### new  Foo()(构造函数)

new操作符的过程：

- 创建一个对象
- 将对象链接到构造函数的原型中，也就是（Foo.prototype）
- 改变tjhis指向（指向了这个空对象）执行构造函数（为对象添加属性）
- 返回这个对象

这个过程改变了this‘的指向，指向这个实例对象，而且这个指向不可更改。

### call、apply、bind等

this取决于调用时的第一个参数。

对一个函数多次使用bind的结果是函数最终的this取决于第一次bind中传进的对象。

不过这里要说一下call，apply，bind的区别。

#### call和apply的区别

- 前者，参数是一个个，传进去；后者是传的是一个数组

#### call、apply和bind的区别

调用bind，不会立即执行，会返回一个函数，这个函数中的中this，指向传进去的第一个参数

### 箭头函数中this

箭头函数是没有this的，他的this其实是词法上下文的this。

具体来说就是：**箭头函数中的 `this` 只取决包裹箭头函数的第一个普通函数的 `this`**。

 我的理解是箭头函数中的this其实函数外部的this，跟函数中没有的变量，会去函数外部寻找是一个道理.

**箭头函数中的this指向的是定义时的this，而不是执行时的this 。绑定后不会再改变**

```javascript
let obj={
 say:()=>{
   console.log(this);  //window
 }
}
//解析：箭头函数无this，所以会去找外面包裹它的那个函数的this，跟它的指向相同，但是因为say直接是一个箭头函数，外部没有普通函数，所以指向了window。

let obj2 = {
 say:function(){
   console.log(this);  //{say：function(){...}}
    let f = () => {
    	console.log(this)
	}
	f();
 }
}
//解析：跟第一种情况相反，外面有普通函数，它当中的this指向了当前的对象。

let obj3={
 say:()=>{
   console.log(this);   //window
   setTimeout(()=>{
		console.log(this);  //window 
	},1000)
 }
}

//解析：一样的规则

let obj4 = {
 say:function(){
   console.log(this);   //{say:function(){...}}
   setTimeout(()=>{
		console.log(this);  //{say:function(){...}}
	},1000)
 }    
}
//跟上面举了一个相反的例子，可以看出，箭头函数中的this是定义时就确定了指向，而不是运行时才确定指向

```



**严格模式下，全局作用中this的指向为undefine**

```javascript
var name = "caibaojian.com"; 
var person = {
  name: "kang",
  pro: {
    name: "Michael",
    getName: function() {
      return this.name;
    }
  }
};
console.log(person.pro.getName()); // Michael
var pepole = person.pro.getName;
console.log(pepole()); // caibaojian.com


var name = "caibaojian.com",
    person = {
      name : "kang",
      getName : function(){
  　    return function(){
    　    return this.name;
  　    };
      }
    };

console.log(person.getName()()); // caibaojian.com


var obj = {
    foo: 'bar',
    func: function(){
        let self = this;
        console.log(this.foo);
        console.log(self.foo);
        (function(){
            console.log(this.foo);
            console.log(self.foo);
        })
    }
}
obj.func()

bar
bar
undefined 
bar

```





```javascript
var obj1={  
    num:4,  
    fn:function(){ 
    console.log(this) 
        var f=function(){      
            console.log(this);
            setTimeout(() => {  
                console.log(this); 
            });  
        }  
        f();  
    }  
}  
obj1.fn();  


var obj1={  
    num:4,  
    fn:function(){  
        var f=() => {      
            console.log(this); 
            setTimeout(function() {  
                console.log(this);
            });  
        }  
        f();  
    }  
}  
obj1.fn();  

```

