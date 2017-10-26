# 主要内容

```
1、为什么响应式web设计需要媒体查询
2、媒体查询的语法
3、如何在link标签、@import语句和css文件中使用媒体查询
4、可供测试的设备特性
5、使用媒体查询根据屏幕空间大小调整视觉小伙
6、应该吧媒体查询写一块、还是哪里需要些写在什么地方
7、理解meta视口标签如何针对IOS和安卓设备启用媒体查询
8、媒体查询未来可能拥有的特性
```

**备注：**_css规范分成很多模块，媒体查询（3级）只是其中一个模块。_

## 为什么响应式web设计需要媒体查询

```
CSS3媒体查询可以让我们针对特定的设备能力或条件为网页应用特定的CSS样式。

官方解释：
    媒体查询包含媒体类型和零个或多个监测媒体特性的表达式。width、height和color都是可用于媒体查询的特性。使用媒体查询，
可以不必修改内容本身，而让网页适配不同的设备。

媒体查询，查询哪些内容？
    屏幕的方向水平或垂直、视口或大或小，等等。通过媒体查询建立逻辑判断
```

## 媒体查询的语法

```
body{
    background-color:orange;
}

@media screen and （min-width：320px）{
    body{
        background-color:yellow;
    }
}

@media screen and （min-width：550px）{
    body{
        background-color:pink;
    }
}

@media screen and （min-width：768px）{
    body{
        background-color:cyan;
    }
}

@media screen and （min-width：980px）{
    body{
        background-color:grey;
    }
}

注意：在针对所有设备的媒体查询中，可以使用简写语法，即省略关键字all（以及紧随其后的and）。换句话说，如果不指定关键字，则关键字是all
```

通过视口尺寸的不同控制了视口的样式，虽然css并不支持真正意义上的条件逻辑但是通过此种方法变向实现了条件逻辑判断

## 在link标签中使用媒体查询

```
可以再<link>标签的media属性中指定设备类型（screen和print），为不同的设备应用样式。

<link rel="stylesheet" type="text/css"  media="screen" href="css文件路径" />

说明：此样式应用在屏幕设备上
    media的属性值:
        screen 屏幕
        screen and （orientation：portrait）  屏幕 且屏幕方向垂直
        not screen and (oriention：portrait) 垂直朝向的非屏幕设备
```

## 组合媒体查询

```
可以将多个媒体查询串在一起。

<link rel="stylesheet" media="screen and (orientation: portrait) and
(min-width: 800px)" href="800wide-portrait-screen.css" />
所有条件成立则应用样式


<link rel="stylesheet" media="screen and (orientation: portrait) and
(min-width: 800px), projection" href="800wide-portrait-screen.css" />
只要有一个条件成立则应用样式
    注意:
        1、逗号分隔每个媒体查询表达式
        2、在projection（投影机）之后没有任何特性/值对。这样省略特定的特性，表示适用于具备任何特性的该媒体类型。在这里表示适用于任何
    投影机

css中的媒体查询可以使用任意的长度单位
```

## css中的单位

```
px 像素
em 1em=16px         1em=父元素的fontsize px

rem root element    而rem是相对于根元素<html>  1rem=根元素（html）的fontsize px
```

## @import 与媒体查询

```
可以再使用@import导入CSS时使用媒体查询，有条件地向当前样式表加载其他样式表。比如，以下代码会导入样式表phone.css,
但条件是必须是屏幕设备，而且视口不超过360像素。

@import url（"phone.css"） screen and （max-width：360px）；

注意：使用CSS中的@import会增加HTTP请求（进而影响加载速度），因此慎用。
```



## 媒体查询可以测试哪些特性

**媒体查询**





















