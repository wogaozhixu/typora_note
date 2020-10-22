# SVG基础分享

## 什么是svg
> Scalable Vector Graphics (SVG)是一种XML语言，类似XHTML，可以用来绘制矢量图形，例如右面展示的图形。SVG可以通过定义必要的线和形状来创建一个图形，也可以修改已有的位图，或者将这两种方式结合起来创建图形。图形和其组成部分可以形变（be transformed）、合成、或者通过滤镜完全改变外观。

![示例图](https://media.prod.mdn.mozit.cloud/attachments/2012/07/09/723/f1db0ea9b8ca438734964d8e8e0e3d73/SVG_Overview.png)

[svg教程](https://www.w3.org/Graphics/SVG/IG/resources/svgprimer.html)


## SVG主要用途
- 1、最适合带有大型渲染区域的应用程序（比如谷歌地图）
- 2、常用图表
- 3、矢量图标
- 4、高保真logo

[svg画廊](http://www1.plurib.us/svg_gallery/)

## SVG的优势
- 文件通常比位图小得多，从而缩短了下载时间；
- 可以缩放图形以适合不同的显示设备，而无需与扩大位图相关联的像素化；
- 图形是在浏览器中构建的，从而减少了通常与Web图像相关的服务器负载和网络响应时间。即，通常将小的公式描述从服务器发送到客户端。然后，客户端根据接收到的公式重建图像；
- 最终用户可以与图形进行交互并更改图形，而无需进行复杂且昂贵的客户端-服务器通信；
- 它为SMIL（同步媒体集成语言）提供了本机支持，这意味着，例如，动画具有更类似的计时概念，从而使程序员摆脱了通常在基于JavaScript的动画中使用的定时循环；
- 它响应JavaScript：HTML环境中使用的相同脚本语言。这意味着两种类型的文档可以交谈，共享信息并相互修改；

>SVG是一种XML语言。原因：首先，该代码倾向于遵循关于如何编写SVG以及客户端软件应该如何响应的商定标准。其次，像所有XML一样，它是用文本编写的，通常不仅可以由机器读取，而且可以由人类读取。第三，也许是最重要的一点，JavaScript可以用于操作对象和文档对象模型，其方式与将JavaScript与HTML结合使用的方式非常相似。

## svg与canvas的区别

| svg                                                 | canvas                                                       |
| --------------------------------------------------- | ------------------------------------------------------------ |
| 不依赖分辨率                                        | 依赖分辨率                                                   |
| 支持事件处理器                                      | 不支持事件处理器                                             |
| 区域渲染能力强                                      | 文本渲染能力弱                                               |
| 复杂度高会减慢渲染速度（任何过度使用dom的都不会快） | 能够以 .png 或 .jpg 格式保存结果图像                         |
| 不适合游戏应用                                      | 最适合图像密集型的游戏，其中的许多对象会被频繁重绘           |
| 可以为某个元素附加js事件                            | 一旦图形被绘制完成后，就不会得到浏览器的继续关注，修改之后需要重新渲染 |
| 在svg中，每个被绘制的图像均可视为对象               | 如果发生位置变化，整个场景都需要重新绘制                     |


## svg基础教程
> 教程目录
> 1. 入门（Getting Started）
> 2. 位置（Positions）
> 3. 基本形状（Basic Shapes）
> 4. 路径（Paths）
> 5. 填充与边框（Fills and Strokes）
> 6. 渐变（Gradients）
> 7. 图案（Patterns）
> 8. 文字（Texts）
> 9. 基本转换（Basic Transformations）
> 10. 裁剪和遮罩（Clipping and masking）
> 11. 其他svg内容（Other content in SVG）
> 12. 滤镜效果（Filter Effects）
> 13. SVG字体（SVG fonts）
> 14. SVG的Image标签（SVG Image tag）
> 15. SVG工具（tool for SVG）

### 1、 入门（Getting Started）
#### 简单示例
```html
<svg 
  version="1.1"
  baseProfile="full"
  width="300" height="200"
  xmlns="http://www.w3.org/2000/svg"
>

  <rect width="100%" height="100%" fill="red" />

  <circle cx="150" cy="100" r="80" fill="green" />

  <text x="150" y="125" font-size="60" text-anchor="middle" fill="white">SVG</text>

</svg>
```

> 绘制流程：根元素设置（必须绑定正确的命名空间-xmlns）--> 绘制矩形<rect/>，背景色为red --> 绘制圆心为（150，100），半径为80，背景色为green的圆形<circle/> --> 绘制填充色为white，内容为svg的文字<text/>

#### SVG文件的基本属性
- 最值得注意的一点是元素的渲染顺序。SVG文件全局有效的规则是“后来居上”，越后面的元素越可见；
- web上的svg文件可以直接在浏览器上展示，或者通过以下几种方法嵌入到HTML文件中；

> svg嵌入到HTML文件中的方式
> 1. 如果HTML是XHTML并且声明类型为application/xhtml+xml，可以直接把SVG嵌入到XML源码中;
> 2. 如果HTML是HTML5并且浏览器支持HTML5，同样可以直接嵌入SVG。然而为了符合HTML5标准，可能需要做一些语法调整;
> 3. 可以通过 object 元素引用SVG文件 
> ```HTML
>   <object data="image.svg" type="image/svg+xml" />
> ```
> 4. 类似的也可以使用 iframe 元素引用SVG文件 
> ```HTML
>   <iframe src="image.svg"></iframe>
> ```
> 5. 理论上同样可以使用 img 元素，但是在低于4.0版本的Firefox 中不起作用
> 6. 最后SVG可以通过JavaScript动态创建并注入到HTML DOM中。 这样具有一个优点，可以对浏览器使用替代技术，在不能解析SVG的情况下，可以替换创建的内容

### 2、 位置（Positions）

#### 网格
> 对于所有元素，SVG使用的坐标系统或者说网格系统，和Canvas用的差不多（所有计算机绘图都差不多）。这种坐标系统是：以页面的左上角为(0,0)坐标点，坐标以像素为单位，x轴正方向是向右，y轴正方向是向下。注意，这和你小时候所教的绘图方式是相反的。但是在HTML文档中，元素都是用这种方式定位的。


```HTML
<rect x="0" y="0" width="100" height="100" />
```
![示例图](https://developer.mozilla.org/@api/deki/files/78/=Canvas_default_grid.png)
> 定义一个矩形，即从左上角开始，向右延展100px，向下延展100px，形成一个100*100大的矩形。

##### 用户单位（"像素"）
> 基本上，在 SVG 文档中的1个像素对应输出设备（比如显示屏）上的1个像素。但是这种情况是可以改变的，否则 SVG 的名字里也不至于会有“Scalable”（可缩放）这个词。如同CSS可以定义字体的绝对大小和相对大小，SVG也可以定义绝对大小（比如使用“pt”或“cm”标识维度）同时SVG也能使用相对大小，只需给出数字，不标明单位，输出时就会采用用户的单位。

在没有进一步规范说明的情况下，1个用户单位等同于1个屏幕单位。要明确改变这种设定，SVG里有多种方法。我们从svg根元素开始：

```HTML
<svg width="100" height="100">
```
上面的元素定义了一个100*100px的SVG画布，这里1用户单位等同于1屏幕单位。
```HTML
<svg width="200" height="200" viewBox="0 0 100 100">
```
这里定义的画布尺寸是200*200px。但是，viewBox属性定义了画布上可以显示的区域：从(0,0)点开始，100宽*100高的区域。这个100*100的区域，会放到200*200的画布上显示。于是就形成了放大两倍的效果。

> 用户单位和屏幕单位的映射关系被称为用户坐标系统。除了缩放之外，坐标系统还可以旋转、倾斜、翻转。默认的用户坐标系统1用户像素等于设备上的1像素（但是设备上可能会自己定义1像素到底是多大）。在定义了具体尺寸单位的SVG中，比如单位是“cm”或“in”，最终图形会以实际大小的1比1比例呈现。

### 3、基本形状（Basic Shapes）

```HTML
<?xml version="1.0" standalone="no"?>
<svg width="200" height="250" version="1.1" xmlns="http://www.w3.org/2000/svg">

  <rect x="10" y="10" width="30" height="30" stroke="black" fill="transparent" stroke-width="5"/>
  <rect x="60" y="10" rx="10" ry="10" width="30" height="30" stroke="black" fill="transparent" stroke-width="5"/>

  <circle cx="25" cy="75" r="20" stroke="red" fill="transparent" stroke-width="5"/>
  <ellipse cx="75" cy="75" rx="20" ry="5" stroke="red" fill="transparent" stroke-width="5"/>

  <line x1="10" x2="50" y1="110" y2="150" stroke="orange" fill="transparent" stroke-width="5"/>
  <polyline points="60 110 65 120 70 115 75 130 80 125 85 140 90 135 95 150 100 145"
      stroke="orange" fill="transparent" stroke-width="5"/>

  <polygon points="50 160 55 180 70 180 60 190 65 205 50 195 35 205 40 190 30 180 45 180"
      stroke="green" fill="transparent" stroke-width="5"/>

  <path d="M20,230 Q40,205 50,230 T90,230" fill="none" stroke="blue" stroke-width="5"/>
</svg>
```
> standalone表示该xml是不是独立的，如果是yes，则表示这个XML文档时独立的，不能引用外部的DTD规范文件；如果是no，则该XML文档不是独立的，表示可以用外部的DTD规范文档。

![基础形状示例](https://developer.mozilla.org/@api/deki/files/359/=Shapes.png)

#### 矩形

```HTML
<rect x="10" y="10" width="30" height="30"/>
<rect x="60" y="10" rx="10" ry="10" width="30" height="30"/>
```
- x：矩形左上角的x位置
- y：矩形左上角的y位置
- width：矩形的宽度
- height：矩形的高度
- rx：圆角的x方位的半径
- ry：圆角的y方位的半径

#### 圆形

```HTML
<circle cx="25" cy="75" r="20"/>
```
- r：圆的半径
- cx：圆心的x位置
- cy：圆心的y位置

#### 椭圆

```HTML
<ellipse cx="75" cy="75" rx="20" ry="5"/>
```
- rx：圆的x半径
- ry：圆的y半径
- cx：圆心的x位置
- cy：圆心的y位置

#### 线条

```HTML
<line x1="10" x2="50" y1="110" y2="150"/>
```
- x1：起点的x位置
- x2：终点的x位置
- y1：起点的y位置
- y2：终点的y位置

#### 折线

```HTML
<polyline points="60 110, 65 120, 70 115, 75 130, 80 125, 85 140, 90 135, 95 150, 100 145"/>
```
- points：点集数列。每个数字用空白、逗号、终止命令符或者换行符分隔开。每个点必须包含2个数字，一个是x坐标，一个是y坐标。所以点列表 (0,0), (1,1) 和(2,2)可以写成这样：“0 0, 1 1, 2 2”。


#### 多边形

```HTML
<polygon points="50 160, 55 180, 70 180, 60 190, 65 205, 50 195, 35 205, 40 190, 30 180, 45 180"/>
```
- 点集数列。每个数字用空白符、逗号、终止命令或者换行符分隔开。每个点必须包含2个数字，一个是x坐标，一个是y坐标。所以点列表 (0,0), (1,1) 和(2,2)可以写成这样：“0 0, 1 1, 2 2”。路径绘制完后闭合图形，所以最终的直线将从位置(2,2)连接到位置(0,0)。

#### 路径

```HTML
<path d="M 20 230 Q 40 205, 50 230 T 90230"/>
```
- d：一个点集数列以及其它关于如何绘制路径的信息。

### 4、路径（Paths）
> __<path>元素是SVG基本形状中最强大的一个。你可以用它创建线条, 曲线, 弧形等等。__<br/>
> 每一个命令都用一个关键字母来表示，比如，字母“M”表示的是“Move to”命令，当解析器读到这个命令时，它就知道你是打算移动到某个点。跟在命令字母后面的，是你需要移动到的那个点的x和y轴坐标。比如移动到(10,10)这个点的命令，应该写成“M 10 10”。这一段字符结束后，解析器就会去读下一段命令。每一个命令都有两种表示方式，一种是用大写字母，表示采用绝对定位。另一种是用小写字母，表示采用相对定位（例如：从上一个点开始，向上移动10px，向左移动7px）。<br/>
> __因为属性d采用的是用户坐标系统，所以不需标明单位。在后面的教程中，我们会学到如何让变换路径，以满足更多需求。__

#### 直线命令

<path>元素里有5个画直线的命令（__大小写命令分别对应绝对定位和相对定位__）

- M x y 或 m dx dy: 从x、y坐标处移动画笔（不会画线）
- L x y (or l dx dy)：在当前位置与新位置之间画线
- H x (or h dx)：绘制水平线 x轴上移动（只带一个参数）
- V y (or h dy)：绘制垂直线 y轴上移动（只带一个参数）
- Z (or z)：闭合路径经常被放到路径的最后（不区分大小写）

![直线示例01](https://developer.mozilla.org/@api/deki/files/45/=Blank_Path_Area.png)
![直线示例02](https://developer.mozilla.org/@api/deki/files/292/=Path_Line_Commands.png)

示例：
```HTML
<!-- 常规路径闭合 -->
<path d="M10 10 H 90 V 90 H 10 Z" fill="transparent" stroke="black"/>
<!-- 相对路径闭合 -->
<path d="M10 10 h 80 v 80 h -80 Z" fill="transparent" stroke="black"/>
```

#### 曲线命令

> ___绘制平滑曲线的命令有三个___，其中两个用来绘制贝塞尔曲线，另外一个用来绘制弧形或者说是圆的一部分。贝塞尔曲线的类型有很多，但是在path元素里，只存在两种贝塞尔曲线：三次贝塞尔曲线C，和二次贝塞尔曲线Q。

##### 1. 贝塞尔曲线

> 用C命令创建三次贝塞尔曲线，需要设置三组坐标参数，即一个点(x, y)和两个控制点--（x1, y1）(x2, y2)。 
> C x1 y1, x2 y2, x y (or c dx1 dy1, dx2 dy2, dx dy) 

![三次贝塞尔曲线（bezier curve）](https://developer.mozilla.org/@api/deki/files/159/=Cubic_Bezier_Curves.png)
```HTML
<?xml version="1.0" standalone="no"?>

<svg width="190px" height="160px" version="1.1" xmlns="http://www.w3.org/2000/svg">

  <path d="M10 10 C 20 20, 40 20, 50 10" stroke="black" fill="transparent"/>
  <path d="M70 10 C 70 20, 120 20, 120 10" stroke="black" fill="transparent"/>
  <path d="M130 10 C 120 20, 180 20, 170 10" stroke="black" fill="transparent"/>
  <path d="M10 60 C 20 80, 40 80, 50 60" stroke="black" fill="transparent"/>
  <path d="M70 60 C 70 80, 110 80, 110 60" stroke="black" fill="transparent"/>
  <path d="M130 60 C 120 80, 180 80, 170 60" stroke="black" fill="transparent"/>
  <path d="M10 110 C 20 140, 40 140, 50 110" stroke="black" fill="transparent"/>
  <path d="M70 110 C 70 140, 110 140, 110 110" stroke="black" fill="transparent"/>
  <path d="M130 110 C 120 140, 180 140, 170 110" stroke="black" fill="transparent"/>

</svg>
```

> 你可以将若干个贝塞尔曲线连起来，从而创建出一条很长的平滑曲线。通常情况下，一个点某一侧的控制点是它另一侧的控制点的对称（以保持斜率不变）。这样，你可以使用一个简写的贝塞尔曲线命令S，如下所示 <br/>
> ```
> S x2 y2, x y (or s dx2 dy2, dx dy)
> ```
> S命令可以用来创建与前面一样的贝塞尔曲线，但是，如果S命令跟在一个C或S命令后面，则它的第一个控制点会被假设成前一个命令曲线的第二个控制点的中心对称点。如果S命令单独使用，前面没有C或S命令，那当前点将作为第一个控制点。下面是S命令的语法示例，图中左侧红色标记的点对应的控制点即为蓝色标记点。

![三次贝塞尔平滑曲线](https://developer.mozilla.org/@api/deki/files/363/=ShortCut_Cubic_Bezier.png)

```HTML
<?xml version="1.0" standalone="no"?>
<svg width="190px" height="160px" version="1.1" xmlns="http://www.w3.org/2000/svg">
  <path d="M10 80 C 40 10, 65 10, 95 80 S 150 150, 180 80" stroke="black" fill="transparent"/>
</svg>
```

> 另一种可用的贝塞尔曲线是二次贝塞尔曲线Q，它比三次贝塞尔曲线简单，只需要一个控制点，用来确定起点和终点的曲线斜率。因此它需要两组参数，控制点和终点坐标。

```
Q x1 y1, x y (or q dx1 dy1, dx dy)
```

![二次贝塞尔曲线](https://developer.mozilla.org/@api/deki/files/326/=Quadratic_Bezier.png)

```HTML
<?xml version="1.0" standalone="no"?>
<svg width="190px" height="160px" version="1.1" xmlns="http://www.w3.org/2000/svg">
  <path d="M10 80 Q 95 10 180 80" stroke="black" fill="transparent"/>
</svg>
```

> 就像三次贝塞尔曲线有一个S命令，二次贝塞尔曲线有一个差不多的T命令，可以通过更简短的参数，延长二次贝塞尔曲线。

```
 T x y (or t dx dy)
```

> 和之前一样，快捷命令T会通过前一个控制点，推断出一个新的控制点。这意味着，在你的第一个控制点后面，可以只定义终点，就创建出一个相当复杂的曲线。需要注意的是，T命令前面必须是一个Q命令，或者是另一个T命令，才能达到这种效果。如果T单独使用，那么控制点就会被认为和终点是同一个点，所以画出来的将是一条直线。

![二次贝塞尔曲线延伸](https://developer.mozilla.org/@api/deki/files/364/=Shortcut_Quadratic_Bezier.png)

```HTML
<?xml version="1.0" standalone="no"?>
<svg width="190px" height="160px" version="1.1" xmlns="http://www.w3.org/2000/svg">
  <path d="M10 80 Q 52.5 10, 95 80 T 180 80" stroke="black" fill="transparent"/>
</svg>
```

> 虽然三次贝塞尔曲线拥有更大的自由度，但是两种曲线能达到的效果总是差不多的。具体使用哪种曲线，通常取决于需求，以及对曲线对称性的依赖程度


##### 2. 弧形

> 弧形命令A是另一个创建SVG曲线的命令。基本上，弧形可以视为圆形或椭圆形的一部分。

```
 A rx ry x-axis-rotation large-arc-flag sweep-flag x y
 a rx ry x-axis-rotation large-arc-flag sweep-flag dx dy
```
- rx：x轴半径
- ry：y轴半径
- x-axis-rotation：x轴旋转角度
- large-arc-flag：角度大小（0表示小角度 1表示大角度）
- sweep-flag：弧线的方向（0表示从起点到终点沿逆时针画弧，1表示从起点到终点沿顺时针画弧）
- x：弧形终点x坐标
- y：弧形终点y坐标

![弧形参数解释图](https://developer.mozilla.org/@api/deki/files/346/=SVGArcs_XAxisRotation.png)

```HTML
<?xml version="1.0" standalone="no"?>
<svg width="320px" height="320px" version="1.1" xmlns="http://www.w3.org/2000/svg">
  <path 
        d="M10 315
           L 110 215
           A 30 50 0 0 1 162.55 162.45
           L 172.55 152.45
           A 30 50 -45 0 1 215.1 109.9
           L 315 10" 
       stroke="black" 
       fill="green" 
       stroke-width="2"
       fill-opacity="0.5"
   />
</svg>
```

> 对于上图没有旋转的椭圆，只有2种弧形可以选择，不是4种，因为两点连线（也就是对角线）正好穿过了椭圆的中心。像下面这张图，就是普通的情况，可以画出两个椭圆，四种弧。

![弧形-解释为何存在多个参数](https://mdn.mozillademos.org/files/15822/SVGArcs_XAxisRotation_with_grid_ellipses.png)

> 上面提到的四种不同路径将由接下来的两个参数决定。如前所讲，还有两种可能的椭圆用来形成路径，它们给出的四种可能的路径中，有两种不同的路径。这里要讲的参数是large-arc-flag（角度大小） 和sweep-flag（弧线方向），large-arc-flag决定弧线是大于还是小于180度，0表示小角度弧，1表示大角度弧。sweep-flag表示弧线的方向，0表示从起点到终点沿逆时针画弧，1表示从起点到终点沿顺时针画弧。下面的例子展示了这四种情况。

![large-arc-flag和sweep-flag参照图](https://developer.mozilla.org/@api/deki/files/345/=SVGArcs_Flags.png)

```HTML
<?xml version="1.0" standalone="no"?>
<svg width="325px" height="325px" version="1.1" xmlns="http://www.w3.org/2000/svg">
  <path d="M80 80
           A 45 45, 0, 0, 0, 125 125
           L 125 80 Z" fill="green"/>
  <path d="M230 80
           A 45 45, 0, 1, 0, 275 125
           L 275 80 Z" fill="red"/>
  <path d="M80 230
           A 45 45, 0, 0, 1, 125 275
           L 125 230 Z" fill="purple"/>
  <path d="M230 230
           A 45 45, 0, 1, 1, 275 275
           L 275 230 Z" fill="blue"/>
</svg>
```

> 弧形可以简单地创建圆形或椭圆形图标，比如你可以创建若干片弧形，组成一个饼图。用路径来绘制完整的圆或者椭圆是比较困难的，因为圆上的任意点都可以是起点同时也是终点，无数种方案可以选择，真正的路径无法定义。通过绘制连续的路径段落，也可以达到近似的效果，但使用真正的circle或者ellipse元素会更容易一些。


#### 5、 填充与边框（Fills and Strokes）
#### 6、 渐变（Gradients）
#### 7、 图案（Patterns）
#### 8、 文字（Texts）
#### 9、 基本转换（Basic Transformations）
#### 10、 裁剪和遮罩（Clipping and masking）
#### 11、 其他svg内容（Other content in SVG）
#### 12、 滤镜效果（Filter Effects）
#### 13、 SVG字体（SVG fonts）
#### 14、 SVG的Image标签（SVG Image tag）
#### 15、 SVG工具（tool for SVG）