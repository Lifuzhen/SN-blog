前端一般处理图片，我首先想到的就是ps。
但是，前端css的filter属性一样可以得到一些意想不到的效果（例如：图片模糊与图片饱和度）
今天我们就来挨个介绍一下这些取值产生的效果
也可以参考[runoob](https://www.runoob.com/cssref/css3-pr-filter.html)

filter(滤镜)

filter的取值有：none | blur() | brightness() | contrast() | drop-shadow() | grayscale() | hue-rotate() | invert() | opacity() | saturate() | sepia() | url();

# none（默认值，没有效果）
```
img{
  filter: none;
}
```
![none](../assets/CSS改变图片颜色的filter(滤镜)属性/none.jpg)

# blur()  (给图像设置高斯模糊)
```
img{
  filter: blur(2px);
}
```
blur(0px-20px)与原图的对比效果:
![blur(0px-20px)与原图的对比效果](../assets/CSS改变图片颜色的filter(滤镜)属性/blur(0px~20px)与原图的对比较过.gif)

#brightness()   (给图片应用一种线性乘法，使其看起来更亮或更暗)

brightness(0%):全黑 
brightness(100%):没有变化
brightness(>100%):图片变得更亮
```
img{
  filter: brightness(50%);
}
```
brightness(100%~0%)与原图的对比效果:
![brightness(100%~0%)与原图的对比效果](../assets/CSS改变图片颜色的filter(滤镜)属性/brightness(100%25~0%25)与原图的对比较过.gif)
# contrast()   (调整图像的对比度)

contrast(0%):全灰
contrast(100%):没有变化
contrast(>100%):图片对比度更明显
```
img{
  filter: contrast(50%);
}
```
contrast(100%~0%)与原图的对比效果:
![contrast(100%~0%)与原图的对比效果](../assets/CSS改变图片颜色的filter(滤镜)属性/contrast(100%25~0%25)与原图的对比较过.gif)


# drop-shadow()    (给图像设置一个阴影效果)
这个取值类似于box-shadow
**drop-shadow(h-shadow v-shadow blur spread color)**
1、<h-shadow> <v-shadow> (必须)
这是设置阴影偏移量的两个 <length>值. <h-shadow> 设定水平方向距离. 负值会使阴影出现在元素左边. <v-shadow>设定垂直距离.负值会使阴影出现在元素上方。查看<length>可能的单位.
如果两个值都是0, 则阴影出现在元素正后面 (如果设置了 <blur> and/or <spread>，会有模糊效果).
2、<blur> (可选)
.值越大，越模糊，则阴影会变得更大更淡.不允许负值 若未设定，默认是0 (则阴影的边界很锐利).
3、<spread> (可选)
 正值会使阴影扩张和变大，负值会是阴影缩小.若未设定，默认是0 (阴影会与元素一样大小). 
*注意: Webkit, 以及一些其他浏览器 不支持第四个长度，如果加了也不会渲染。*
4、<color> (可选)
查看 <color>该值可能的关键字和标记。若未设定，颜色值基于浏览器。在Gecko (Firefox), Presto (Opera)和Trident (Internet Explorer)中， 会应用colorcolor属性的值。另外, 如果颜色值省略，WebKit中阴影是透明的。
```
img{
  filter: drop-shadow(2px 4px 6px #000);
}
```
drop-shadow(2px 4px 6px #000)的效果图:
![drop-shadow(2px 4px 6px #000)的效果图](../assets/CSS改变图片颜色的filter(滤镜)属性/drop-shadow(2px%204px%206px%20%23000).jpg)


# grayscale()   (将图像转换为灰度图像)
grayscale(0%):无变化
grayscale(100%):灰度图片
grayscale(>100%):跟100%的效果一致
```
img{
  filter: grayscale(50%);
}
```
grayscale(0%~100%)与原图的对比效果:
![grayscale(0%~100%)与原图的对比效果](../assets/CSS改变图片颜色的filter(滤镜)属性/grayscale(0%25~100%25)与原图的对比较过.gif)


# hue-rotate()   (给图像应用色相旋转)
hue-rotate(0deg):无变化
hue-rotate(180deg):变化
hue-rotate(360deg):无变化
hue-rotate(361deg)的效果等同于hue-rotate(1deg)的效果
0~360deg为一个周期
```
img{
  filter: hue-rotate(50deg);
}
```
hue-rotate(0deg~360deg)与原图的对比效果:
![hue-rotate(0deg~360deg)与原图的对比效果](../assets/CSS改变图片颜色的filter(滤镜)属性/hue-rotate(0deg~360deg)与原图的对比较过.gif)

# invert()   (反转输入图像)
invert(0%):无变化
invert(100%):完全反转
invert(>100%):跟100%的效果一致
```
img{
  filter: invert(50%);
}
```
invert(0%~100%)与原图的对比效果:
![invert(0%~100%)与原图的对比效果](../assets/CSS改变图片颜色的filter(滤镜)属性/invert(0%25~100%25)与原图的对比较过.gif)

# opacity()   (转化图像的透明程度)
opacity(0%):完全透明
opacity(100%):无变化
opacity(>100%):跟100%的效果一致
该值类似与opacity属性
```
img{
  filter: opacity(50%);
}
```
opacity(100%~0%)与原图的对比效果:
![opacity(100%~0%)与原图的对比效果](../assets/CSS改变图片颜色的filter(滤镜)属性/opacity(100%25~0%25)与原图的对比较过.gif)

# saturate()   (转换图像饱和度)
saturate(0%):完全不饱和
saturate(100%):无变化
saturate(>100%):更高的饱和度
```
img{
  filter: saturate(50%);
}
```
saturate(0%~200%)与原图的对比效果:
![saturate(0%~200%)与原图的对比效果](../assets/CSS改变图片颜色的filter(滤镜)属性/saturate(0%25~200%25)与原图的对比较过.gif)

# sepia()   (将图像转换为深褐色)
```
img{
  filter: sepia(0%);
}
```
sepia(0%~100%)与原图的对比效果:
![sepia(0%~100%)与原图的对比效果](../assets/CSS改变图片颜色的filter(滤镜)属性/sepia(0%25~100%25)与原图的对比较过.gif)

# url()   (URL函数接受一个XML文件，该文件设置了 一个SVG滤镜，且可以包含一个锚点来指定一个具体的滤镜元素。)
SVG滤镜资源是指以xml文件格式定义的svg滤镜效果集，可以通过URL引入并且通过锚点（#element-id）指定具体的一个滤镜元素
用法：filter: url(svg-url#element-id)

svg-xml文件
```
<svg version="1.1"
     xmlns="http://www.w3.org/2000/svg"
     xmlns:xlink="http://www.w3.org/1999/xlink"
     xmlns:ev="http://www.w3.org/2001/xml-events"
     baseProfile="full">
    <defs>
        <!-- 此处定义滤镜 -->
        <filter id="blur">
            <feGaussianBlur stdDeviation="4" result="blur"/>  
            <!-- feGaussianBlur(滤镜): 该滤镜对输入图像进行高斯模糊 -->
            <feOffset in="blur" dx="4" dy="4" result="offsetBlur"/>
            <!-- feOffset(模糊)：创建阴影效果 -->
        </filter>
    </defs>
</svg>
```
```
img{
  filter: url("./svg.xml#blur");
}
```
url()效果图
![url.jpg](../assets/CSS改变图片颜色的filter(滤镜)属性/url.jpg)

