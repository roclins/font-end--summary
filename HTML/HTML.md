### 常用HTML标签

#### head区

- meta
- title
- style
- link
- script
- base

##### meta

`<meta>`元素可提供有关页面的元信息（meta-information），比如针对搜索引擎和更新频度的描述和关键词。

`<meta> `标签必须位于文档的头部，不包含任何内容。`<meta> `标签的属性定义了与文档相关联的名称/值对。

| 属性            | 值                                                           | 描述                                       |
| --------------- | ------------------------------------------------------------ | ------------------------------------------ |
| content（必须） | some_text                                                    | 定义与 http-equiv 或 name 属性相关的元信息 |
| http-equiv      | content-type<br />  expires <br /> refresh  <br />set-cookie | 把 content 属性关联到一个名称              |
| name            | author <br /> description<br />  keywords  <br />generator <br /> revised <br /> others | 把 content 属性关联到一个名称              |

##### base 

base 可以设置整体链接的打开状态   

base 写到  <head>  </head>  之间

```
<base target="_blank"></base>
```

把所有的连接 都默认添加 target="_blank"

#### body区

```html
a[href,target]

//在新标签页打开
<a href="http://www.baidu.com" target="_blank">百度</a>
//在本页面跳转
<a href="http://www.baidu.com" target="_self">百度</a>
//锚点跳转---->HTML5不支持
<a href="#C4">Chapter 4</a>
<a name="C4"></a>
```

```
table[align bgcolor cellspace cellpadding] 
td[colspan rowspan]  column->列  row->行
```

```
表单提交
form[action->提交到的页面 methods->提交方式 enctype->指定编码，如果上传文件指定要用form-data]
表单元素要有 name属性
```

```html
<form action="..." method="post">
    <!-- <input type="text" name="key1" id=""> -->
    <!-- <input type="password" name="key1" id="">
    <input type="email" name="key1" id="">
    <input type="number" name="key1" id="">
    <input type="number" name="key1" id=""> -->
    <!-- <textarea name="key2" id="" cols="30" rows="10"></textarea> -->

    <!-- 当表单中使用了 radio ，一定要为相同 name 的 radio 设置不同的 value，让服务端可以辨别 -->
    性别
    <label><input type="radio" name="gender" value="male"> 男</label>
    <label><input type="radio" name="gender" value="female"> 女</label>

    <br>

    <!-- checkbox 如果没有选中则不会提交，如果选中提交 on -->
    <label><input type="checkbox" name="agree" value="true"> 同意协议</label>

    <br>

    <label><input type="checkbox" name="funs[]" value="football"> 足球</label>
    <label><input type="checkbox" name="funs[]" value="basketball"> 篮球</label>
    <label><input type="checkbox" name="funs[]" value="earth"> 地球</label>

    <br>


    <select name="status">
      <option>激活</option>
      <option>未激活</option>
      <option value="1">待激活</option>
    </select>


    <br>

    <input type="file" name="" id="">
    
    <button>提交</button>

  </form>
```

```html
label[for]
<label for="name">姓名</label>
<input type="text" id="name" value="Bob"/>

<label><input type="text" id="name" value="Bob"/>姓名</label>
```

### 常见面试题

##### HTML、XHTM、HTML的关系

- `HTML`属于`SGML`
- `XHTML`属于`XML`，是`HTML`进行`XML`严格化的结果
- `HTML5`不属于`SGML`或者`XML`，比`XHTML`宽松

##### DOCTYPE有什么作用？标准模式与怪异模式如何区分？它们有何意义?

告诉浏览器使用哪个版本的HTML规范来渲染文档。DOCTYPE不存在或形式不正确会导致HTML文档以怪异模式呈现。
标准模式（Standards mode）以浏览器支持的最高标准运行；怪异（兼容）模式（Quirks mode）中页面是一种比较宽松的向后兼容的方式显示。

##### HTML5为什么只需要写 <!DOCTYPE html>

HTML5不基于SGML（Standard Generalized Markup Language 标准通用标记语言），因此不需要对DTD（DTD 文档类型定义）进行引用，但是需要DOCTYPE来规范浏览器行为。

HTML4.01基于SGML，所以需要引用DTD。才能告知浏览器文档所使用的文档类型，如下：
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">

##### 行内元素有哪些？块级元素有哪些？ 空(void)元素有那些

行内元素：`a span img input select` 
块级元素：`div ul ol li dl dt dd h1 p`
空元素：`<br> <hr> <link> <meta>`

`HTML5`中的块元素：

| 标签    | 意义                   |
| ------- | ---------------------- |
| nav     | 导航                   |
| header  | 头部                   |
| main    | 主体                   |
| aside   | 侧边栏，一般放于main中 |
| article | 文章                   |
| section | 页面区段               |
| footer  | 脚部                   |
| audio   | 音频                   |
| video   | 视频                   |
| address | 联系地址方式           |
| canvas  | 绘制图形               |
| pre     | 预格式化文本           |
| form    | 表单                   |
| table   | 表格                   |
| thead   | 表头                   |
| tbody   | 表格主题               |

##### 对浏览器内核的理解

主要分成两部分：渲染引擎(Layout Engine或Rendering Engine)和JS引擎。

渲染引擎：负责对网页语法的解释并渲染（显示）网页 。浏览器的内核的不同对于网页的语法解释会有不同，所以渲染的效果也不相同。

JS引擎：解析和执行javascript来实现网页的动态效果。

最开始渲染引擎和JS引擎并没有区分的很明确，后来JS引擎越来越独立，内核就倾向于只指渲染引擎。

##### 常见的浏览器内核

1. Trident：IE MaxThon TT The World 360 搜狗浏览器
2. Geckos：FireFox Mozilla Suite/SeaMonkey
3. Webkit：Safari 
4. Blink：Opare Chrome

##### HTML语义化的理解

- 开发者容易理解
- 机器容易理解结构(搜索、读屏软件)
- 有助于`SEO`

##### title与h1的区别、b与strong的区别、i与em的区别

title属性没有明确意义，只表示标题；h1表示层次明确的标题，对页面信息的抓取也有很大的影响
strong标明重点内容，语气加强含义；b是无意义的视觉表示
em表示强调文本；i是斜体，是无意义的视觉表示
视觉样式标签：`b i u s`
语义样式标签：`strong em ins del code`

### HTML5

##### HTML5有哪些新特性,移除了那些元素？如何处理HTML5新标签的浏览器兼容问题？如何区分HTML和HTML5

新增加了图像、位置、存储、多任务等功能。
新增元素：

1. canvas
2. 用于媒介回放的video和audio元素
3. 本地存储。localStorage长期存储数据，浏览器关闭后数据不丢失;sessionStorage的数据在浏览器关闭后自动删除
4. 语意化更好的内容元素，比如 article footer header nav section
5. 位置API：Geolocation
6. 表单控件，calendar date time email url search
7. 新的技术：web worker(web worker是运行在后台的 JavaScript，独立于其他脚本，不会影响页面的性能。您可以继续做任何愿意做的事情：点击、选取内容等等，而此时 web worker 在后台运行) web socket
8. 拖放API：drag、drop

移除的元素：

1. 纯表现的元素：basefont big center font s strike tt u
2. 性能较差元素：frame frameset noframes

区分：

1. DOCTYPE声明的方式是区分重要因素
2. 根据新增加的结构、功能来区分