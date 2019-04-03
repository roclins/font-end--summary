使用Bootstrap可以很轻易的完成响应式开发

- Bootstrap使用步骤总结
- 栅格布局

### Bootstrap使用步骤总结

1. 基本模板

   ```html
   <!--h5文档申明-->
   <!DOCTYPE html>
   <!--文档语言申明  en zh-CN zh-tw -->
   <html lang="zh-CN">
   <head>
       <!--文档编码申明-->
       <meta charset="utf-8">
       <!--要求当前网页使用浏览器最高版本的内核来渲染-->
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <!--视口的设置：视口的宽度和设备一致，默认的缩放比例和PC端一致，用户不能自行缩放-->
       <meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=0">
       <!-- 上述3个meta标签*必须*放在最前面，任何其他内容都*必须*跟随其后！ -->
       <!-- 优先加载和浏览器解释 -->
   
       <title>title</title>
   
       <!-- Bootstrap 核心样式-->
       <link href="../lib/bootstrap/css/bootstrap.css" rel="stylesheet">
       <!-- html5shiv 和  respond 分别用来解决IE8版本浏览器不支持 H5标签和媒体查询的  不兼容问题-->
       <!-- HTML5 shiv and Respond.js for IE8 support of HTML5 elements and media queries -->
       <!-- 警告：不能以file形式打开，本地打开。最好http://打开 -->
       <!-- WARNING: Respond.js doesn't work if you view the page via file:// -->
       <!-- 在 IE 9 一下引入-->
       <!--[if lt IE 9]>
       <script src="../lib/html5shiv/html5shiv.min.js"></script>
       <script src="../lib/respond/respond.min.js"></script>
       <![endif]-->
   ```

2. 看到设计，首先要联想到哪些是bootstrap中有的，去教程中找到对应的部分的代码

   ```html
   <nav class="navbar navbar-default">
     <div class="container-fluid">
       <!-- Brand and toggle get grouped for better mobile display -->
       <div class="navbar-header">
         <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1" aria-expanded="false">
           <span class="sr-only">Toggle navigation</span>
           <span class="icon-bar"></span>
           <span class="icon-bar"></span>
           <span class="icon-bar"></span>
         </button>
         <a class="navbar-brand" href="#">Brand</a>
       </div>
   
       <!-- Collect the nav links, forms, and other content for toggling -->
       <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
         <ul class="nav navbar-nav">
           <li class="active"><a href="#">Link <span class="sr-only">(current)</span></a></li>
           <li><a href="#">Link</a></li>
           <li class="dropdown">
             <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">Dropdown <span class="caret"></span></a>
             <ul class="dropdown-menu">
               <li><a href="#">Action</a></li>
               <li><a href="#">Another action</a></li>
               <li><a href="#">Something else here</a></li>
               <li role="separator" class="divider"></li>
               <li><a href="#">Separated link</a></li>
               <li role="separator" class="divider"></li>
               <li><a href="#">One more separated link</a></li>
             </ul>
           </li>
         </ul>
         <form class="navbar-form navbar-left">
           <div class="form-group">
             <input type="text" class="form-control" placeholder="Search">
           </div>
           <button type="submit" class="btn btn-default">Submit</button>
         </form>
         <ul class="nav navbar-nav navbar-right">
           <li><a href="#">Link</a></li>
           <li class="dropdown">
             <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">Dropdown <span class="caret"></span></a>
             <ul class="dropdown-menu">
               <li><a href="#">Action</a></li>
               <li><a href="#">Another action</a></li>
               <li><a href="#">Something else here</a></li>
               <li role="separator" class="divider"></li>
               <li><a href="#">Separated link</a></li>
             </ul>
           </li>
         </ul>
       </div><!-- /.navbar-collapse -->
     </div><!-- /.container-fluid -->
   </nav>
   ```

3. 分析代码，熟悉各部分代码的作用，便于我们改造代码

   ```html
   <nav class="navbar navbar-default">
       <!-- 导航的内容容器 -->
       <div class="container">
           <!-- 包含 商标区域 和 切换按钮（在移动端显示） -->
           <div class="navbar-header">
               <!--切换按钮-->
               <!--
               类名：collapsed  样式
               属性：
               data-toggle="collapse"  申明是什么组件=折叠组件
               data-target="#bs-example-navbar-collapse-1" 控制的目标元素=选择器
               其他：
               aria-expanded="false"  aria-* 代表提供给屏幕阅读器使用的（盲人阅读器）
               class="sr-only" screen read only  代表提供给屏幕阅读器使用的（盲人阅读器）
               -->
               <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1">
                   <span class="icon-bar"></span>
                   <span class="icon-bar"></span>
                   <span class="icon-bar"></span>
               </button>
               <!--商标区域-->
               <a class="navbar-brand" href="#">Brand</a>
           </div>
           <!-- 导航连接  表单  其他内容  被切换 -->
           <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
               <!--默认的导航-->
               <ul class="nav navbar-nav">
                   <li class="active"><a href="#">Link</a></li>
                   <li><a href="#">Link</a></li>
                   <li><a href="#">Link</a></li>
                   <li><a href="#">Link</a></li>
                   <li><a href="#">Link</a></li>
                   <li><a href="#">Link</a></li>
               </ul>
               <!--右对齐的导航-->
               <ul class="nav navbar-nav navbar-right">
                   <li><a href="#">Link</a></li>
               </ul>
           </div>
       </div>
   </nav>其中：
   ```

4. 处理选择器层级问题
   如果我们想要添加自己的样式，可以添加自己的类名，但是这样有可能会出现选择器的层级问题：即可能我们自己添加的样式不起效果等。
   解决方法：

   1. 找到所使用的class

      bootstrap中的样式都是按照模块来划分的：

      ```css
      .navbar-default {
        background-color: #f8f8f8;
        border-color: #e7e7e7;
      }
      .navbar-default .navbar-brand {
        color: #777;
      }
      .navbar-default .navbar-brand:hover,
      .navbar-default .navbar-brand:focus {
        color: #5e5e5e;
        background-color: transparent;
      }
      .navbar-default .navbar-text {
        color: #777;
      }
      .navbar-default .navbar-nav > li > a {
        color: #777;
      }
      .navbar-default .navbar-nav > li > a:hover,
      .navbar-default .navbar-nav > li > a:focus {
        color: #333;
        background-color: transparent;
      }
      .navbar-default .navbar-nav > .active > a,
      .navbar-default .navbar-nav > .active > a:hover,
      .navbar-default .navbar-nav > .active > a:focus {
        color: #555;
        background-color: #e7e7e7;
      }
      .navbar-default .navbar-nav > .disabled > a,
      .navbar-default .navbar-nav > .disabled > a:hover,
      .navbar-default .navbar-nav > .disabled > a:focus {
        color: #ccc;
        background-color: transparent;
      }
      .navbar-default .navbar-toggle {
        border-color: #ddd;
      }
      .navbar-default .navbar-toggle:hover,
      .navbar-default .navbar-toggle:focus {
        background-color: #ddd;
      }
      .navbar-default .navbar-toggle .icon-bar {
        background-color: #888;
      }
      .navbar-default .navbar-collapse,
      .navbar-default .navbar-form {
        border-color: #e7e7e7;
      }
      .navbar-default .navbar-nav > .open > a,
      .navbar-default .navbar-nav > .open > a:hover,
      .navbar-default .navbar-nav > .open > a:focus {
        color: #555;
        background-color: #e7e7e7;
      }
      @media (max-width: 767px) {
        .navbar-default .navbar-nav .open .dropdown-menu > li > a {
          color: #777;
        }
        .navbar-default .navbar-nav .open .dropdown-menu > li > a:hover,
        .navbar-default .navbar-nav .open .dropdown-menu > li > a:focus {
          color: #333;
          background-color: transparent;
        }
        .navbar-default .navbar-nav .open .dropdown-menu > .active > a,
        .navbar-default .navbar-nav .open .dropdown-menu > .active > a:hover,
        .navbar-default .navbar-nav .open .dropdown-menu > .active > a:focus {
          color: #555;
          background-color: #e7e7e7;
        }
        .navbar-default .navbar-nav .open .dropdown-menu > .disabled > a,
        .navbar-default .navbar-nav .open .dropdown-menu > .disabled > a:hover,
        .navbar-default .navbar-nav .open .dropdown-menu > .disabled > a:focus {
          color: #ccc;
          background-color: transparent;
        }
      }
      .navbar-default .navbar-link {
        color: #777;
      }
      .navbar-default .navbar-link:hover {
        color: #333;
      }
      .navbar-default .btn-link {
        color: #777;
      }
      .navbar-default .btn-link:hover,
      .navbar-default .btn-link:focus {
        color: #333;
      }
      .navbar-default .btn-link[disabled]:hover,
      fieldset[disabled] .navbar-default .btn-link:hover,
      .navbar-default .btn-link[disabled]:focus,
      fieldset[disabled] .navbar-default .btn-link:focus {
        color: #ccc;
      }
      ```

      结构很清晰，选择器都是配套的

   2. 将根选择器替换成我们自己的选择，加上自定义的样式
      因为index.css是在bootstrap.css后引入的，所以即使是相同的权重下，根据层叠性，也可以覆盖之前的样式

   3. 在浏览器中快速定位CSS属性，在对应的位置修改

#### 注意

- sr-xxx，aria，rode等属性都是给屏幕阅读器器用的，删掉也可以
- 最重要的是弄清楚这些class是是什么样式，有些值可以选
- data-一般是跟JS相关

### 栅格布局

```html
<div class="container">
    <!--栅格系统：其实就是行和列的布局，网格状布局-->
    <!--行：row-->
    <!-- .container容器默认有15px的左右内间距  .row 填充父容器的15px的左右内间距   margin-left,margin-right -15px拉伸 -->
    <div class="row">
        <!--列：col-*-*  *不确定（参数） -->
        <!--
            col：列样式
            第一个*：屏幕的大小
            大屏设备     lg   大屏设备以上生效包含本身
            中屏设备     md   中屏设备以上生效包含本身
            小屏设备     sm   小屏设备以上生效包含本身
            超小屏设备   xs   超小屏设备以上生效包含本身
            第二个*：每一行的分等份，默认分成12等份 ，数字代表的是占多少份
        -->
        <div class="col-xs-4"></div>
        <div class="col-xs-4"></div>
        <div class="col-xs-4"></div>
    </div>
</div>
```

```html
<div class="container">
    <div class="row">
        <!--栅格嵌套-->
        <div class="col-xs-4">
            <div class="row">
                <div class="col-xs-6"></div>
                <div class="col-xs-6"></div>
            </div>
        </div>
        <!--列的偏移-->
        <div class="col-xs-4">
            <div class="row">
                <div class="col-xs-3"></div>
                <div class="col-xs-6 col-xs-offset-1"></div>
            </div>
        </div>
        <!--列的排序-->
        <div class="col-xs-4">
            <div class="row">
                <!--
                push 往后推
                pull 往前拉
                -->
                <div class="col-xs-3 col-xs-push-9">col-xs-3</div>
                <div class="col-xs-9 col-xs-pull-3">col-xs-9</div>
            </div>
        </div>
    </div>
</div>
```