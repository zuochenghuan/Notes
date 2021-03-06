# 前端知识点总结（CSS篇）

1. **圣杯布局**
2. **CSS合并方法**
3. **盒子模型**
4. **CSS定位**
5. **CSS动画原理**
6. **CSS3动画（简单动画的实现，如旋转等）**
7. **CSS不同选择器的权重(CSS层叠的规则)**
8. **flexbox布局**
9. **块级元素和行内元素的异同**
10. **CSS在性能优化方面的实践（比方说选择器的效率等）**
11. **CSS打包压缩的方法**
12. **使用CSS预处理的优缺点（比方说Sass和Compass等）**
13. **{ box-sizing: border-box; }这条CSS规则是干嘛的，有什么优点**
14. **CSS浮动的原理及清除浮动的方法及优缺点**
15. **CSS垂直居中的方法**
16. **base64的原理及优缺点**
17. **CSS reset和normalize的区别**
18. **link和@import的区别**
19. **左右上下margin合并重合的问题**
20. **rem字体大小设置**
21. **CSS3新增的特性**
22. **列出你所知道可以改变页面布局的属性**
23. **多人协作时，怎么避免样式被覆盖**

## 新增
2018-08-14

1. 盒模型，box-sizing
2. CSS3新特性，伪类，伪元素，锚伪类
3. CSS实现隐藏页面的方式
4. 如何实现水平居中和垂直居中。
5. 说说position，display
6. 请解释*{box-sizing:border-box;}的作用，并说明使用它的好处
7. 浮动元素引起的问题和解决办法？绝对定位和相对定位，元素浮动后的display值
8. link和@import引入css的区别
9. 解释一下css3的flexbox，以及适用场景
10. inline和inline-block的区别
11. 哪些是块级元素那些是行级元素，各有什么特点
12. grid布局
13. table布局的作用
14. 实现两栏布局有哪些方法？
15. css dpi
16. 你知道attribute和property的区别么
17. css布局问题？css实现三列布局怎么做？如果中间是自适应又怎么做？
18. 流式布局如何实现，响应式布局如何实现
19. 移动端布局方案
20. 实现三栏布局（圣杯布局，双飞翼布局，flex布局）
21. 清除浮动的原理
22. overflow:hidden有什么缺点？
23. padding百分比是相对于父级宽度还是自身的宽度
24. css3动画，transition和animation的区别，animation的属性，加速度，重力的模拟实现
25. CSS 3 如何实现旋转图片（transform: rotate）
26. sass less
27. 对移动端开发了解多少？（响应式设计、Zepto；@media、viewport、JavaScript 正则表达式判断平台。）
28. 什么是bfc，如何创建bfc？解决什么问题？
29. CSS中的长度单位（px,pt,rem,em,ex,vw,vh,vh,vmin,vmax）
30. CSS 选择器的优先级是怎样的？
31. 雪碧图
32. svg
33. 媒体查询的原理是什么？
34. CSS 的加载是异步的吗？表现在什么地方？
35. 常遇到的浏览器兼容性问题有哪些？常用的hack的技巧
36. 外边距合并
37. 解释一下"::before"和":after"中的双冒号和单冒号的区别



++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

1. **圣杯布局**  
   答案：[圣杯布局](http://chen106106.iteye.com/blog/1631865) [参考资料](http://alistapart.com/article/holygrail)  

2. **CSS合并方法**  
   答案：避免使用@import引入多个css文件，可以使用CSS工具将CSS合并为一个CSS文件，例如使用Sass\Compass等。  

3. **盒子模型**  
   答案：参考HTML中第11题。  

4. **CSS定位**  
   答案：[Position各属性值详解](http://www.cnblogs.com/fsjohnhuang/p/3967350.html)　　
   [CSS中的绝对定位与相对定位](http://www.cnblogs.com/jiqing9006/archive/2012/07/26/2610586.html),注意的是定位的参照：relative参照于自己该出现的位置，而absolute参照于祖先元素中与自己最近的已定位元素(relative或者absolute)直到body元素。

5. **CSS动画原理**  
   答案：挤压与拉伸、预期、舞台布局、顺利动画与关键帧、动作跟随与重叠、慢进慢出、弧形移动  
   [CSS 动画指南： 原理和实战 ](http://www.uml.org.cn/html/201110311.asp)  
   [英文原版](https://www.smashingmagazine.com/2011/09/the-guide-to-css-animation-principles-and-examples/#more-105335)

6. **CSS3动画（简单动画的实现，如旋转等）**  
  答案：依靠CSS3中提出的三个属性：transition、transform、animation。  
  **transition**：定义了元素在变化过程中是怎么样的，包含transition-property、transition-duration、transition-timing-function、transition-delay。  
  **transform**：定义元素的变化结果，包含rotate、scale、skew、translate。  
  **animation**：动画定义了动作的每一帧（@keyframes）有什么效果，包括animation-name，animation-duration、animation-timing-function、animation-delay、animation-iteration-count、animation-direction。  
  具体可以参考一下三篇文章：  
  [CSS3 Transition](http://www.w3cplus.com/content/css3-transition)  
  [CSS3 Transform](http://www.w3cplus.com/content/css3-transform)  
  [CSS3 Animation](http://www.w3cplus.com/content/css3-animation)  

7. **CSS不同选择器的权重(CSS层叠的规则)**  
   答案：首先，找出所有应用到该标签的所有规则。然后按照下面的规则进行应用：1、！important规则最重要，大于其它规则；2、行内样式规则，加1000；3、对于选择器中给定的各个ID属性值，加100；4、对于选择器中给定的各个类属性、属性选择器或者伪类选择器，加10；5、对于选择其中给定的各个元素标签选择器，加1；6、通配符和结合符给予特殊性没有任何贡献；7、如果权值一样，则按照样式规则的先后顺序来应用，顺序靠后的覆盖靠前的规则。记住，CSS中选择器的优先级是先判断高位的数字，如果相等，才会继续判断低位的数字，如果高位分出大小了，就不考虑低位了。

8. **flexbox布局及相关设置**  
    答案：简单描述一下flex的属性，细节可以参考链接文档  
    容器属性（采用Flex布局的元素，container）：  
    **flex-direction**：决定主轴的方向（即项目的排列方向）；row | row-reverse | column | column-reverse;  
    **flex-wrap**：设置是否换行；nowrap | wrap | wrap-reverse  
    **flex-flow**：flex-direction属性和flex-wrap属性的简写形式，flex-direction || flex-wrap  
    **justify-content**：定义了项目在主轴上的对齐方式；flex-start | flex-end | center | space-between | space-around  
    **align-items**：定义项目在交叉轴上如何对齐；flex-start | flex-end | center | baseline | stretch  
    **align-content**：定义了多根轴线的对齐方式；flex-start | flex-end | center | space-between | space-around | stretch  

    项目属性（子元素为项目，item）
    **order**：定义项目的排列顺序。数值越小，排列越靠前，默认为0。  
    **flex-grow**：定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。  
    **flex-shrink**：定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。  
    **flex-basis**：定义了在分配多余空间之前，项目占据的主轴空间。  
    **flex**：flex-grow, flex-shrink 和 flex-basis的简写。  
    **align-self**：允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。  

    [Flex 布局教程：语法篇](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)  
    [Flex 布局教程：实例篇](http://www.ruanyifeng.com/blog/2015/07/flex-examples.html)

9. **块级元素和行内元素的异同**  
    答案：块级元素：header/p/div/form/table/footer....；行内元素：span/a/strong/em/input...
    1.块级元素分行，行内元素不分行；  
    2.块级元素可以包含块级元素和行内元素，行内元素只能包含行内元素，不能包含块级元素；  
    3.行内元素设置width、height、margin的上下、padding的上下无效；
    4.行内元素可以通过设置display：block，渲染为块级元素。

10. **CSS在性能优化方面的实践（比方说选择器的效率等）**  
    答案：网络层面：css压缩与合并、Gzip压缩；加载方式：css文件放在head里、不要用@import；语法结构：尽量用缩写、避免用滤镜、合理使用选择器。  
    可参考[CSS性能优化策略](http://fengzheqi.com/2016/03/06/CSS%E6%80%A7%E8%83%BD%E4%BC%98%E5%8C%96%E7%AD%96%E7%95%A5/)

11. **CSS打包压缩的方法与异同**  
    答案：利用打包工具grunt/gulp。  
    易于使用：采用代码优于配置策略，Gulp让简单的事情继续简单，复杂的任务变得可管理。
    高效：通过利用Node.js强大的流，不需要往磁盘写中间文件，可以更快地完成构建。
    高质量：Gulp严格的插件指导方针，确保插件简单并且按你期望的方式工作。
    易于学习：通过把API降到最少，你能在很短的时间内学会Gulp。构建工作就像你设想的一样：是一系列流管道。

12. **使用CSS预处理的优缺点（比方说Sass和Compass等）**  
    答案：Css预处理器定义了一种新的语言将Css作为目标生成文件，然后开发者就只要使用这种语言进行编码工作了。预处理器通常可以实现浏览器兼容，变量，结构体等功能，代码更加简洁易于维护。让你用一种编程语言的思维来写CSS样式。但是带来的缺点是需要增加设计工作以及学习熟悉成本。  

13. **{ box-sizing: border-box; }这条CSS规则是干嘛的，有什么优点**  
    答案：[让CSS布局更加直观：box-sizing](http://www.cnblogs.com/front-Thinking/p/4394901.html)

14. **CSS浮动的原理及清除浮动的方法及优缺点**  
    答案：而此浮动元素在文档流空出的位置，由后续的(非浮动)元素填充上去：块级元素直接填充上去，若跟浮动元素的范围发生重叠，浮动元素覆盖块级元素。内联元素：有空隙就插入。给元素的float属性赋值后，就是脱离文档流，进行左右浮动，紧贴着父元素(默认为body文本区域)的左右边框。  
    [css-float浮动的深入研究、详解及拓展](http://www.zhangxinxu.com/wordpress/2010/01/css-float%E6%B5%AE%E5%8A%A8%E7%9A%84%E6%B7%B1%E5%85%A5%E7%A0%94%E7%A9%B6%E3%80%81%E8%AF%A6%E8%A7%A3%E5%8F%8A%E6%8B%93%E5%B1%95%E4%B8%80/)  
    [那些年我们一起清除过的浮动](http://www.iyunlu.com/view/css-xhtml/55.html)  
    [css清除浮动各种方法](http://www.cnblogs.com/mizzle/archive/2011/07/14/2105961.html)

15. **CSS水平垂直居中的方法**  
    答案：[CSS垂直居中总结](http://www.cnblogs.com/dojo-lzz/p/4419596.html)

16. **base64的原理及优缺点**  
    答案：优缺点如下，原理参考文章  
    **优点**可以加密，减少了http请求，图片更新没有上传和清缓存了；  
    **缺点**是需要消耗CPU进行编解码、增大了CSS、浏览器兼容方面吧。  
    [从原理上搞定编码-- Base64编码](http://www.cnblogs.com/chengxiaohui/articles/3951129.html)  
    [关于base64编码的原理及实现](http://www.cnblogs.com/hongru/archive/2012/01/14/2321397.html)  
    [小tip: base64:URL背景图片与web页面性能优化](http://www.zhangxinxu.com/wordpress/2012/04/base64-url-image-%E5%9B%BE%E7%89%87-%E9%A1%B5%E9%9D%A2%E6%80%A7%E8%83%BD%E4%BC%98%E5%8C%96/)

17. **CSS reset和normalize的区别**  
    答案：reset是将浏览器所有的默认样式进行重置、覆盖，normalize是保留原来浏览器的样式并且尽量在不同浏览器里保持一致。  
    可以参考知乎上的问题[Normalize.css 与传统的 CSS Reset 有哪些区别？](http://www.zhihu.com/question/20094066)

18. **link和@import的区别**  
    答案：本质上他们都是为了引入外部css样式的，但是有区别如下：  
    1.link属于XHTML标签，而@import完全是CSS提供的一种方式。  
    2.加载顺序的差别。当一个页面被加载的时候（就是被浏览者浏览的时候），link引用的CSS会同时被加载，而@import引用的CSS 会等到页面全部被下载完再被加载。所以有时候浏览@import加载CSS的页面时开始会没有样式（就是闪烁），网速慢的时候还挺明显。  
    3.兼容性的差别。由于@import是CSS2.1提出的所以老的浏览器不支持，@import只有在IE5以上的才能识别，而link标签无此问题。  
    4.使用dom控制样式时的差别。当使用javascript控制dom去改变样式的时候，只能使用link标签，因为@import不是dom可以控制的。  

19. **左右上下margin合并重合的问题**  
    答案：上下margin重合，并选取最大的作为间距。左右margin不合并，间距等于相加。
    也可以参考：  
    [CSS 外边距(margin)重叠及防止方法](http://www.hujuntao.com/web/css/css-margin-overlap.html)  
    [W3C  8.3.1 Collapsing margins](https://www.w3.org/TR/2011/REC-CSS2-20110607/box.html#collapsing-margins)  

20. **rem字体大小设置**  
    答案： rem其实就是相对根元素<html>的相对值，具体可参考：  
    [CSS3的REM设置字体大小](http://www.w3cplus.com/css3/define-font-size-with-css3-rem)

21. **CSS3新增的特性**  
    答案：[深入了解 CSS3 新特性](http://www.ibm.com/developerworks/cn/web/1202_zhouxiang_css3/index.html)

22. **列出你所知道可以改变页面布局的属性**  
    答案：position、display、float、width、height、margin、padding、top、left、right、bottom，欢迎继续补充。

23. **多人协作时，怎么避免样式被覆盖**  
    答案：团队之间制定良好的CSS规范，可以参考：[web前端代码规范--CSS篇](http://fengzheqi.com/2016/03/06/web%E5%89%8D%E7%AB%AF%E4%BB%A3%E7%A0%81%E8%A7%84%E8%8C%83--CSS%E7%AF%87/)
