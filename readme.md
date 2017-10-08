##1. 搭建项目目录
1. HTML    核心文件    index.html
2. CSS    控制样式
    - base.css（基础样式）
    - global.css（全局样式）
3. images    存放图片的文件夹
4. JS    视频音频等……（不涉及）

##2. 引入样式文件
在`<head>`标签中设置：
```html
    <link rel="stylesheet" href="css/base.css"/>
    <link rel="stylesheet" href="css/index.css"/>
```

##3. 引入图标
1. 自定义图标需要注意的问题
    - 文件格式问题
    - 文件大小问题

1. 下载
    - 京东：www.jd.com/favicon.ico     能下载京东图标
    - 所有：网站名（带www.）/favicon.ico    下载所有网站的图标
    - 比特虫，在线制作ico图标：bitbug.net
    
2. 引入
    - `<link rel="shortcut icon" href="favicon.ico"/>`
    - 网站名：bitbug.net
    - `<link rel="shortcut icon" href="favicon.ico"/>`

##4. 初始化
- 见base.css
- 注：
    1. 为什么不用*？  全部设置，加载速度慢

##5. 分析布局
- 见图片：(/images/readme-1.png)

##6. 导航栏编写
###6.1 知识点
1. 文字居中问题
- text-align:center;  缺陷：只能上下左右都居中
- padding-left/padding-right  解决上面缺陷
- 定位、margin  尽量不用（能用标准流就不用定位）

2. 向下的小三角做法
- 用一个菱形，在一个盒子里面向上移动，使其上半部被隐藏，只留下下半部分，就是向下的小三角
- 不用精灵图的原因：图片加载效率低
```css
    .site-nav-send i {
        position: absolute;
        top: 12px;
        right: 8px;
        width: 15px;
        height: 7px;
        overflow: hidden;
    }
    .site-nav-send s {
        position: absolute;
        top: -7px;
        font: 400 13px/15px "consolas";
    }
```
3. 初始化的类名，不可以出现在下面写的类名中

4. 权限 优先级
```
    div a span    1
    .box .site-nav    10
    #box #site    100
    <div style="width……    1000
    !important    1/0
```

5. 设置右边的内容
    1. 有小菱形
    2. li要跟对应的send标签公用代码
    3. i和s标签共用一样的代码

6. 顶部广告栏


7. 盒子稳定性问题（logo位置）
    - 只给宽高的盒子（宽/高都剩余法）
    - 给padding的盒子
    - 给margin的盒子（不继承，不稳定，容易塌陷）

8. logo制作
    - 设置文字、链接、首页
    - 文字移除：text-indent: -9999em;  值不能太大，会出bug
    - 出bug的：-9999999em  、 -99999999px
    
9. 光标变化
    - cursor: pointer;  小手
    - cursor: text;  光标
    - cursor: move;  四角箭头
    - cursor: default;  变成小白

10. 关于浮动：
    - 一个盒子里面的子盒子，要么都浮动，要么都不浮动，原则问题
    - 有时不浮动会出错。
    - 浮动不占位置，位置不够宽，掉下来
    - 浮动的盒子遮挡不住标准流的盒子(文字)

##7. 底部编写 footer
###7.1 清除浮动
- 问题：父盒子高度为0，子盒子不占位置，子盒子不会撑开父盒子。因此下面的标准流盒子会跑到父盒子的子盒子下边
- 解决：清楚浮动（清除子盒子因为浮动，对父子造成的影响）
- 使用方法：谁出现问题，给谁加.clearfix类名
- 清除浮动的其他方法
    1. clear: both;
    2. overflow: hidden;
    3. 单伪元素标签法：
        `.clearfix:after {
            content: "";
            height: 0;
            visibility: hidden;
            overflow: hidden;
            display: block;
            clear: both;  /*核心元素*/
        }
        .clearfix {
            zoom: 1;/*IE678*/
        }`
    4. 双伪元素标签法
        `.clearfix:before,  .clearfix:after {
            content: "";
            display: table;
        }
        .clearfix:after {
            clear: both; 
        }
        .clearfix {
            zoom: 1;/*IE678*/
        }`

###7.2 设置slogan
- 将第三个作为基准，设置left: 50%
- 其他的以它为准设置margin
- 这样就可以保证窗口大小改变时slogan的位置不变

- 注意两点：
    1. 父盒子继承浏览器的宽度，使得slogan不随浏览器窗口大小而改变位置
    2. 父盒子定位为left:50%，其它对应盒子用margin-left定位到制定位置

###7.3 shopping写法
dl>dt>dd
h3>p
h3和dt共用style：
    ```.footer-top-shopping dt,
       .coverage h3{
           height: 34px;
           font: 400 16px/34px "microsoft yahei";
       }
    ```

###7.4 电脑组成
- CPU：电脑的大脑   i3/i5/i7  amd  龙芯2s/服务器/中标麒
- 硬盘：存储数据（永久存储）
- 显卡：图形显示
- 内存：存储数据（暂时性存储）（堆和栈）
- 驱动：让硬件和系统的兼容性更好（触摸板驱动--影响开发速度）

###7.5 层级
1. 必须有定位，不能是static
2. 用z-index来控制层级数

###7.6 浮动的盒子会互相影响，不管盒子是否被撑开
1. 有高度会被撑破
2. 没有高度会被撑开
3. 一定不要让浮动的盒子超出父盒子！！

###7.7 鼠标放在div上，a链接变色
```
    .shortcut-nav-menu-one div:hover {
        background-color: #fff;
    }
    .shortcut-nav-menu-one div:hover a {
        color: #b61d1d;
    }
```

###7.8 隐藏盒子问题
1. overflow：hidden;	    隐藏盒子超出的部分。
2. display: none;    隐藏盒子，而且不占位置。(用的最多)
3. visibility: hidden;    隐藏盒子，而且占位置。
4. opacity: 0;    隐藏盒子，而且占位置。
5. Position/top/left/...-999px    隐藏盒子，而且占位置。

###7.9 注意

```
javascript:void(0);  //关闭页面的跳转
<a href=""></a>   //刷新页面
```
```
//阻止a链接跳转
<a href="javascript:void(0)">你好</a>
<a href="javascript:;">你好</a>
```

###7.10 定位权限问题
left>right
top>bottom

##8. 层级（难点）
- 对于标准流、浮动、定位的盒子，后边盒子都会压住前面
- 浮动盒子会压住标准流
- 定位会压住浮动
- 层级高低和占位无关
- 用法：
    1. 必须有定位。（除去static之外）。
    2. 给定z-index的值为层级的值。（不给默认为0）
        - （层级为0的盒子，也比标准流和浮动高。）
        - （层级为负数的盒子，比标准流和浮动低。）
        - （层级不取小数）
        - （层级一样，后面的盒子比前面的层级高。）
        - （浮动或者标准流的盒子，后面的盒子比前面的层级高。）

- 定位中：abselute是不占位置的，relative是站位的的。而层级的高低，是和占不占位置没有关系的。

