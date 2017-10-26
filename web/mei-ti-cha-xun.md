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
```



