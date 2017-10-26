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

媒体查询中用的最多特性是视口宽度\(width）

```
width:视口宽度
height：视口高度
device-width：渲染表面的宽度（可以认为是设备的屏幕宽度）
device-height：渲染表面的高度（可以认为是设备的屏幕高度）
orientation：设备方向是水平还是垂直
aspect-ratio：视口的宽高比。 16:9 的宽屏显示器可以写成aspect-ratio：16/9
color：颜色组分的位深。比如min-color:16 表示设备至少支持16位深
color-index：设备颜色查找表中的条目数，值必须是数值，且不能为负。
monochrome：单色帧缓冲中表示每个像素的位数，值必须是数值（整数），比如
monochrome: 2，且不能为负。
resolution：屏幕或打印分辨率，比如min-resolution: 300dpi。也可以接受每厘
米多少点，比如min-resolution: 118dpcm。
scan：针对电视的逐行扫描（progressive）和隔行扫描（interlace）。例如720p HD TV（720p
中的p表示progressive，即逐行）可以使用scan: progressive来判断； 而1080i HD TV
（1080i中的i表示interlace，即隔行）可以使用scan: interlace来判断。
grid：设备基于栅格还是位图。
上面列表中的特性，除scan和grid外，都可以加上min或max前缀以指定范围。看看下面的
代码：
@import url("tiny.css") screen and (min-width:200px) and (maxwidth:
360px);
这里使用最大宽度（max-width）和最小宽度（min-width）设定了范围。因此，tiny.css
只在设备视口介于200像素和360像素之间时才会被应用。
```

## 通过媒体查询修改设计

```
css的工作原理： 当样式不冲突时，样式重叠。当样式冲突时，位于下方的样式会覆盖上方的样式，除非上方的样式更高级或者更具体。

设计原则：
    1、设计一套基准样式，将其应用给不同版本的设计方案。这套样式表确保用户的基准体验。
    2、通过媒体查询覆盖央视表中相关的部分。

注意：
    1、任何的CSS都可以放在媒体查询里面
    2、针对高分辨率设备的媒体查询
        @media （min-resolution:2dppx）{
            样式
        }

        这里的媒体查询只针对每像素单位为2点（2dppx）的屏幕。
    3、使用媒体查询链接不同的CSS文件
        从浏览器的角度看，CSS属于"阻塞渲染"资源。换句话说，浏览器需要下载并解析链接的CSS文件，然后再渲染页面。
        阻塞渲染仅是指该资源是否会暂停浏览器的首次页面渲染。无论CSS是否阻塞渲染，CSS资源都会被下载，只是说非阻塞
        性资源的优先级比较低而已。
    4、浏览器的特性
        所有链接的文件都会被下载下来，只是如果有的文件不必立即应用，那浏览器就不会让他影响页面的渲染。
```

## 分隔媒体查询的利弊

```
编写多个媒体查询文件有好处，但是我并不建议这么做，因为多一个文件就要多一个HTTP请求，HTTP请求多了会明显影响页面加载速度
。此时我认为应该跟关注网站的整体性能，做好相应的设备性能测试然后在决定。我不会做相应的测试，而我关注的是：
    1、所有的图片都压缩过了
    2、所有的脚本都拼接缩短了
    3、所有资源都采用了gzip压缩
    4、所有静态内容都缓存到了CDN
    5、所有多余的CSS规则都被清除了。
```

## 关于视口的meta标签

```
为了利用媒体查询，应该让小屏幕以其原生大小来显示网页，而不是在980px宽的窗口渲染好，让用户去放大或缩小。
meta标签是网页与移动浏览器的借口。网页通过这个标签告诉移动浏览器，他希望浏览器如何渲染当前页面。
这个视口<meta >标签应该放在HTML的<head>标签中。可以在其中设置具体的宽度（比如使用像素单位），
或者设置一个比例（比如2.0，即实际大小的两倍）。
    例： 变为实际大小的二倍
    <meta name="viewport" content="initial-scale=2.0,width=device-width">
```































































































































































































