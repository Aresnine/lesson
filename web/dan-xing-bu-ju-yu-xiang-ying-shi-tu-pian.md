# 说明

```
1、网站的宽度大都以百分比形式定义。百分比布局使得网页宽度能够随着查看他们的屏幕窗口大小变化，因而得名弹性布局。

2、弹性布局解决的问题：媒体查询断点之间的平滑过渡

3、本章内容

        1、将固定像素大小转换为比例大小
        2、已有CSS布局机制及其不足之处
        3、理解Flexible Box Layout Module及其优点
        4、实现分辨率切换以及响应式图片的正确方法
```

# 1、将固定像素大小转换为弹性比例大小

```
公式：结果=目标/上下文
```

## 1-1、响应式web设计的核心技术

```
1、将固定大小转换为比例大小
2、使用媒体查询相对于视口大小应用CSS规则
```

## 1-2、为什么需要Flexbox

### **现有布局技术（行内块、浮动和表格）的缺点**

**行内块与空白**

```
1、使用行内块布局的最大问题就是在HTML元素间渲染空白
2、在行内块不居中让内容居中
3、不够智能---两个相邻元素一个固定宽度，另一个自动填充剩余空间
```

**浮动**

```
1、由于浏览器在取整方面的不一致，导致浮动在设置百分比的时候，出现不同浏览器显示不同的效果
2、必须清除浮动，才能避免对其他元素的影响
```

**表格与表元**

```
别把display:table;和display:table-cell;与对应的HTML元素搞混，这两个CSS属性只是用于模仿他们是好兄弟的。
实际上，他们不会真正影响HTML的结构。

1、每个项目外都需要包一层（要想完美居中表元必须在表格中）
2、不可以将设置为display:table-cell的项目包到多行上。
```

**Flexbox**

```
方便地垂直居中内容
改变元素的视觉顺序
在盒子里自动插入空白以及对其元素，自动对齐元素间的空白
```

# 2、Flexbox的前缀

```
flex在使用的时候，由于新特性的原因需要加上前缀
    -ms-      是    Microsof
    -webkit-  是    WebKit
    -moz-     是    Mozilla

可以使用工具 Autoprefixer

sublime Text https://github.com/sindresorhus/sublime-autoprefixer
```

# 3、使用Flexbox

**flexbox的4个关键特性：方向、对齐、次序和弹性。**

---

**完美文本居中**

```css
.one{
    backgorund-color:indigo;
    color:#ebebeb;
    font-size:2rem;
    display:flex;
    align-items:center;
    justify-content:center;
}
```

```
说明：
    display:flex;这是flexbox的根本所在，把当前元素设置为一个flexbox（不是block或inline-block之类的）
    align-items:这是要在flexbox沿交叉轴对齐项目（在这个例子中垂直居中文本）
    justify-content：在这里设置内容沿主轴居中
```

---

**偏移**

_正序_

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>flex弹性布局2----自定义导航栏---正序</title>
    <style type="text/css">
        div{
            display: flex;
            align-items:center;
            padding:10px;
        }

        a{
            margin-right:20px;

        }

        #last{
            /*auto会导致最后的a标签使用所有剩余的外边距*/
            margin-left:auto;
        }


    </style>
</head>
<body>
    <div>
        <a href="">111</a>
        <a href="">222</a>
        <a href="">333</a>
        <a href="">444</a>
        <a id="last" href="">555</a>
    </div>


</body>
</html>
```

_反序_

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>flex弹性布局2----自定义导航栏---反序1</title>
    <style type="text/css">
        div{
            display: flex;
            align-items:center;
            padding:10px;
            /*设定主轴的方向*/
            flex-direction:row-reverse;
        }

        a{
            margin-left:20px;

        }

        #last{

            margin-right:auto;
        }


    </style>
</head>
<body>
    <div>
        <a href="">111</a>
        <a href="">222</a>
        <a href="">333</a>
        <a href="">444</a>
        <a id="last" href="">555</a>
    </div>


</body>
</html>
```

_垂直_

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>flex弹性布局2----自定义导航栏---垂直</title>
    <style type="text/css">
        div{
            display: flex;
            align-items:center;
            padding:10px;
            /*flex-direction:column;*/
            flex-direction:column-reverse;


            /*row：
                主轴与行内轴方向作为默认的书写模式。即横向从左到右排列（左对齐）。
            row-reverse：
                对齐方式与row相反。
            column：
                主轴与块轴方向作为默认的书写模式。即纵向从上往下排列（顶对齐）。
            column-reverse：
                对齐方式与column相反。*/

        }




    </style>
</head>
<body>
    <div>
        <a id="first" href="">111</a>
        <a href="">222</a>
        <a href="">333</a>
        <a href="">444</a>
        <a  href="">555</a>
    </div>


</body>
</html>
```

_**垂直响应式**_

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>flex弹性布局x-----响应布局</title>
    <style type="text/css">
        div{
            display: flex;
            /*align-items:center;*/
            padding:10px;

            height:50px;


            background-color:#666;
        }

        a{
            /*margin-left:20px;*/
            width:50px;
            height:60px;
            text-decoration:none;
            background-color:yellowgreen;
            font-size:25px;
            line-height:60px;

        }

        @media (min-width:320px){
            div{
                flex-direction:column;
                align-items:left;

            }
        }

        @media (min-width:550px){
            div{
                /*flex-direction:column-reverse;*/
                align-items:right;
                background-color:green;
            }
        }

        @media (min-width:768px){
            div{
                flex-direction:row;
                /*align-items:center;*/
                background-color:green;
            }

            a{
                margin-right:20px;

            }

            #last{
                margin-left:auto;
            }
        }


        @media (min-width:980px){
            div{
                flex-direction:row-reverse;
                align-items:center;
                background-color:green;
            }

            a{
                margin-left:20px;

            }

            #last{
                margin-right:auto;
                margin-left:0px;
            }
        }




    </style>
</head>
<body>
    <div>
        <a  href="">111</a>
        <a  href="">222</a>
        <a  href="">333</a>
        <a  href="">444</a>
        <a  href="" id='last'>555</a>
    </div>


</body>
</html>
```

**注意**

```
要想垂直反序堆叠，只要改成flex-direction:column-reverse;

要知道，有一个flex-flow属性，是flex-direction和flex-wrap的合体。比如，flex-flow：row wrap；就是把方向（flex-direction）
设置为行(row),把折行选项设置为折行（wrap）。不过，至少一开始分别设置两个属性会更清楚一些。另外，flex-wrap属性在最早的Flexbox
实现中也不存在，如果合起来写，在某些浏览器中可能导致整条声明失效。
```

### 不同媒体查询中的不同Flexbox布局

**例子：垂直居中对齐**

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>flex弹性布局2----自定义导航栏---垂直</title>
    <style type="text/css">
        div{
            display: flex;
            align-items:center;
            padding:10px;
            /*flex-direction:column;*/
            flex-direction:column-reverse;


            /*row：
                主轴与行内轴方向作为默认的书写模式。即横向从左到右排列（左对齐）。
            row-reverse：
                对齐方式与row相反。
            column：
                主轴与块轴方向作为默认的书写模式。即纵向从上往下排列（顶对齐）。
            column-reverse：
                对齐方式与column相反。*/

        }




    </style>
</head>
<body>
    <div>
        <a id="first" href="">111</a>
        <a href="">222</a>
        <a href="">333</a>
        <a href="">444</a>
        <a  href="">555</a>
    </div>


</body>
</html>
```

**例子：窄视口中让各项垂直堆叠，而在空间允许的情况下改成行式布局**

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>flex弹性布局x-----响应布局</title>
    <style type="text/css">
        div{
            display: flex;
            /*align-items:center;*/
            padding:10px;

            height:50px;


            background-color:#666;
        }

        a{
            /*margin-left:20px;*/
            width:50px;
            height:60px;
            text-decoration:none;
            background-color:yellowgreen;
            font-size:25px;
            line-height:60px;

        }

        @media (min-width:320px){
            div{
                flex-direction:column;
                align-items:left;

            }
        }

        @media (min-width:550px){
            div{
                /*flex-direction:column-reverse;*/
                align-items:right;
                background-color:green;
            }
        }

        @media (min-width:768px){
            div{
                flex-direction:row;
                /*align-items:center;*/
                background-color:green;
            }

            a{
                margin-right:20px;

            }

            #last{
                margin-left:auto;
            }
        }


        @media (min-width:980px){
            div{
                flex-direction:row-reverse;
                align-items:center;
                background-color:green;
            }

            a{
                margin-left:20px;

            }

            #last{
                margin-right:auto;
                margin-left:0px;
            }
        }




    </style>
</head>
<body>
    <div>
        <a  href="">111</a>
        <a     href="">222</a>
        <a  href="">333</a>
        <a  href="">444</a>
        <a  href="" id='last'>555</a>
    </div>


</body>
</html>
```

### 行内伸缩

**Flexbox与有与inline-block和inline-table对应的inline-flex变体。得益于他的居中能力，通过行内伸缩模型可以轻松实现一些搞怪效果，比如：**

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>行内伸缩</title>
    <style type="text/css">
        p{
            display:inline-flex;
            align-items:center;
            height:200px;
            padding:0 40px;
            background-color:indigo;
            border-radius:20px;
            color:#ddd;
        }
    </style>
</head>
<body>
    <p>supreman is my hero!</p>
</body>
</html>
```

**注意：**

```
如果将某个元素无端地设为display：inline-flex（比如包含该元素的元素没有被设置为display:flex）,那么这个元素就会像
inline-block和inline-table一样保留元素间的空白。如果这个元素处于一个Flexbox中，空白就会消失，就跟table中的table-cell一样
```

##### **行内伸缩的例子2 说明上面的注意**

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>行内收缩</title>
    <style type="text/css">
        /*div{

            display:flex;
        }*/

        /*
            注意：如果inline-flex不在flexbox中则会保留元素之间的空白，但是如果它在一个flexbox元素中，则会取消空白
        */
        a{
            display:inline-flex;
            align-items:center;
            width:200px;
            height:300px;
            background-color:pink;
            padding:0 12px;
            border-radius:6px;
            margin:10px;
        }
    </style>
</head>
<body>
    <div>
        这是一个行内测试----》<a href="xxoo.com" >xxoo</a><a href="xxoo.com" >xxoo</a><a href="xxoo.com" >xxoo</a><a href="xxoo.com" >xxoo</a><a href="xxoo.com" >xxoo</a>
    </div>
</body>
</html>
```

## Flexbox的对齐 {#图形说明}

**flexbox的对齐最重要的是理解坐标轴。有两个坐标轴，“主轴”和“交叉轴”。这两个轴代表什么取决于Flexbox排列的方向。比如**

**如果将Flexbox的方向设为row，则主轴就是横轴，而交叉轴就是纵轴。反之，如果将flexbox的方向设为column，则主轴就是纵轴，而交叉轴为横轴。**

---

## align-items

```
align-items在交叉轴上定位元素
```

## align-self

```
有时候，可能只需要把某一个元素按不同方式对齐。这个元素可以使用align-self属性决定自己的对齐方式。
```

## 交叉抽的对齐

```
Flexbox为交叉对齐提供了以下元素
    1、flex-start：让元素从flexbox的起始边开始
    2、flex-end：会沿Flexbox父元素的末尾对齐该元素
    3、center：把元素放在Flexbox元素的中间
    4、baseline：让Flexbox元素中的所有项沿基线对齐
    5、stretch：让Flexbox中所有项（没交叉轴）拉伸至与父元素一样大
```

## justify-content

```
控制沿Flexbox主轴对齐的属性是justify-content（对于非Flexbox/块级元素，也已经有了关于justify-self属性的建议）。
justify-content属性值：
    1、flex-start
    2、flex-end
    3、center
    4、space-between 在子元素之间添加相同的空白
    5、space-around  在子元素两边（两端，浏览器的边缘处）添加相同的空白
```

**案例**

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>flexbox的交叉轴对齐方式----align-items</title>
    <style type="text/css">
        /*
            flex-direction决定主轴在什么地方默认为row水平 column垂直
            align-items在交叉轴上定位元素

            交叉轴的对齐方式：
                flex-start：把元素的对齐设置为flex-start，可以让元素从Flexbox父元素的起始边
                flex-end：把元素的对齐设置为flex-end，会沿Flexbox父元素的末尾对齐该元素。
                center：把元素放在Flexbox元素的中间。
                baseline：让Flexbox元素中的所有项沿基线对齐。
                stretch：让Flexbox中的所有项（没交叉轴）拉伸至与父元素一样大。
开始。
        */
        #wrapper{
            background-color:indigo;
            width:400px;
            height:200px;
            display:flex;
            /*flex-direction:column;*/
            /*flex-direction:row-reverse;*/
            /*align-items:center;*/
            /*align-items:flex-end;*/
            align-items:start;
        }

        #inner1{
            color:white;
            width:200px;
            height:100px;
            display:flex;
            background-color:green;
        }

        .inner{
            /*
                清除弗雷元素对本身的影响
            */
            align-self:flex-end;
        }

    </style>
</head>
<body>
    <div id='wrapper'>
        <div id='inner1'>
            flexbox对齐方式最重要的就是理解坐标轴。
        </div>
        <div class='inner'>
        flexbox有两个轴，一个主轴一个交叉轴。
        这两个轴代表什么取决于flexbox的方向设置。
        </div>
        <div >
        当flexbox的方向设为row，则主轴就是x轴，交叉轴就是y轴。
        当flexbox的方向设为column，则主轴就是y轴，交叉轴就是x轴。
        </div>
    </div>
</body>
</html>
```

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>主轴对齐</title>
    <style type="text/css">
        /*
            justify-content控制主轴对齐方式
            属性值为：
                flex-start
                center
                flex-end
                space-between（[speɪs]）
                space-around

                所以justify-content可以告诉浏览器怎么处理其余空间。space-between会在子元素之间添加相同宽度的空白，而space-around则在它们两边各添加相同宽度的空白

        */
        .father{
            width:100%;
            height:300px;
            background-color:indigo;
            display:flex;
            /*justify-content:space-between;*/
            justify-content:space-around;
        }

        .child{
            width:25%;
            height:100px;
            background-color:green;
            color:red;
        }
    </style>
</head>
<body>
    <div class='father'>
        <div class='child'>111111111111111111111111111111</div>
        <div class='child'>222222222222222222222222222222</div>
        <div class='child'>333333333333333333333333333333</div>
    </div>
</body>
</html>
```

## Flex

```
flex-item定义过宽度，除了width，还可以通过flex属性来定义宽度，或者叫“伸缩性（flexiness）”

例子：
    div{
        border: 1px solid #ebebeb;
        background-color: #34005B;
        display: flex;
        height: 100px;
        flex: 1;
    }

这里的flex实际上是三个属性合体的简写：flex-grow、flex-shrink和flex-basis    

    flex：  1      1    100
            |      |     |
            |      |     |
            伸展   收缩  基准
```

对于伸缩项，如果flex属性存在（且浏览器支持 ），则使用它的值控制元素的大小，忽略宽度和高度值的设置，即使他们的声明

位于flex声明之后，也会被忽略。

```
flex-grow：当前元素在空间润徐德情况下最大的伸展量

flex-shrink：空间不足时，元素的收缩量

flex-basis：伸缩的基准值
```

```
<!DOCTYPE html>
<html >
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
    /*

    flex是flex-grow、flex-shrink和flex-basis的缩写
        flex-grow:可伸展性
        flex-shrink：可伸缩性
        flex-basis：基准值


    flex: 1 2 auto的意思是在有空间的情况下可以伸展1部分，在空间不足时可以收缩1部分，而基准大小是内容的固有宽度（即不伸缩的情况下内容的大小）。
    flex: 0 0 50px的意思是，这个伸缩项既不伸也不缩，基准为50像素（即无论是否存在自由空间，都是50像素）。那么flex: 2 0 50%呢？意思就是会多占用两个可用空间，不收缩，基准为50%。但愿这几个例子能帮大家理解flex属性。

    */

        .wapper{
            width:100%;
            display:flex;
            border:1px solid red;

        }
        .items {
            border: 1px solid #ebebeb;
            background-color: #34005B;
            display: flex;
            height: 100px;
        }
        .a {
            flex: 2 0 auto;
        }
        .b,.c {
            flex: 1 0 auto;
        }
    </style>
</head>
<body>
    <div class="wapper">
        <div class="items a">1111111111
        </div>
        <div class="items b">2222222222
        </div>
        <div class="items c">3333333333333
        </div>
    </div>
</body>
</html>
```

## 简单的粘附页脚

```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>简单的粘附页脚</title>
	<style type="text/css">
		/*
			实验方法
				1、将p标签减少，则会看到页脚在最底层
				2、如果p标签足够多，则页脚会出现在内容的下面

			实验原理
				原理是flex属性会让内容在空间允许的情况下伸展。因为页面主体是伸缩容器，最小高度是100%，所以主内容区会尽可能占据所有有效空间。完美！
		*/
		*{
			margin:0;
			padding:0;
		}
		html{
			height:100%;
		}

		body{
			color:#666;
			display:flex;
			flex-direction:column;
			min-height:100%;

		}

		.mainContent{
			flex:1;
			color:#333;
			padding:20px;
		}

		.footer{
			background-color:violet;
		}
	</style>
</head>
<body>
	<div class="mainContent">
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>
		<p>这是主体内容</p>

	</div>
	<div class='footer'>
		这是页脚
	</div>
</body>
</html>
```

**原理：这个例子的原理是flex属性会让内容空间允许的情况下伸展。因为页面主体是伸缩容器，最小高度是100%，**

**所以主内容区会尽可能占据所有有效空间**

---



