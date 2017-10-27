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

```



