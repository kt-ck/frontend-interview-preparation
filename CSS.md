# CSS

1. 逻辑值

   当书写模式改变时， 为了页面能够随之改变，就需要设计逻辑值。

   writing-mode： horizontal-tb, vertical-rl, vertical-lr;

   常见的逻辑值：

   width(inline-size)、height(block-size)、top(block-start)、left(inline-start)、padding-left(padding-inline-start)

   逻辑值参考：

   https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Logical_Properties

   

2. 背景

   background: url('') background-location / background-size background-repeat, ......;

   background-attachment: scroll(一直不变), fixed(页面滑动，他就滑动，内容滑动， 他不滑动), local(内容滑动， 他就滑动，页面滑动，不滑动) 



3. 溢出
   1. 采用overflow，设置为hidden、scroll
   
4. BEM

   1. 块元素采用.blockname
   2. 块内的元素采用.blockname__elementname
   3. 具体元素采用.blockname__elementname--mod

5. SCSS

   1. 导入其他_xx.scss文件  

      @import "xx";

   2. 定义变量

      $variableName: ;

   3. 定义map

      $mapName: (

      ​    key: value;

      )

      调用： map-get(mapName, key)

   4. @mixin mixinName($variableName: default){

      ​    @if $variable {

      ​          ....

      ​     }

      ​	@content; // 调用时候的content

      }

      调用：@include mixinName(variable){

      ​    	 ....    

      ​    } 

   5. @function func($variableName){

      ​	@return ;

      ​    }

      调用： func(variable)

   6. 特殊符号
      1. &：当前对象
      2. #{&}：

   7. 继承 

      @extend .className;

   8. CSS布局

      1. flex
         1. 默认的flex：flex-direction(row), align-items: stretch
         2. 换行： flex容器设置为flex-wrap: wrap;flex子项设置为：flex: 1 300px;(先分配300px，然后再均匀分配) 
         3. flex-flow: 是flex-direction 和flex-wrap的合体。
         4. flex的全写：flex-grow，flex-shrink，flex-basis
         5. align-items: 在交叉轴上的位置， center(居中)、align-start、align-end、stretch。flex子项可以单独设置self-align修改自己在交叉轴上的位置。
         6. justify-content: 在主轴上的位置。flex-start、flex-end、center、space-around、space-between
         7. order：不改变dom树的情况下，改变顺序，默认为0，可以有负值
         8. flex-basis：max-width/min-width > flex-basis > width > box
      2. grid
         1. 默认的grid： 一列，
         2. grid-template-columns: 300px repeat(3, 1fr 2fr)（repeat(auto-fill, minmax(100px, 1fr)) 至少100px，自动填满）;
         3. grid-column-gap、grid-row-gap、grid-gap(gap为了兼容);
         4. grid-auto-rows: 隐式网格
         5. grid-template-areas:  “grid-area ” "...."; 
            1. 横跨多个格子， 重复写他的grid-area名字
            2. 所有名字只能在连续区域，不能在不同位置
            3. 一个连续区域必须是矩形
            4. 使用 . 可以让格子留空
      3. 多列布局
         1. 采用column-count，或者column-width（至少多宽），
   
   9. float
   
      1. 父元素坍缩问题。
         1. 创建空的div元素，清除浮动
         2. 父元素创建after伪类，表现为块，清除浮动。
         3. overflow:设置为auto、hidden。
   
   10. 定位
       1. 静态定位： 默认行为
       2. 相对定位： top、bottom、left、right对正常文档流的位置进行偏移
       3. 绝对定位： 不在正常的文档流内，他在初始化容器中，他离左上边界有30px的距离，相对于html标签或者最近的定位祖先。
       4. 定位上下文： 在父元素设置position:relative, 子元素就可以相对于父元素的绝对定位。
       5. 固定定位：表现和绝对定位类似， 但是相对于浏览器视口本身。
       6. sticky: 是相对定位和固定定位的混合体，当他滚动到某个阈值的时候，表现得像固定定位
   
   11. checkbox hack
   
       html: 
   
       ```html
       <input type="checkbox" id="toggle"/>
       
       <label for="toggle"></label>
       ```
   
       css:
   
       ```css
       label:checked ~ input{
           ....
       }
       ```
   
   12. 响应式布局
   
       1. 媒体查询
          1. 媒体类型：all、speech、screen、print
          2. 媒体特性 https://developer.mozilla.org/zh-CN/docs/Web/CSS/Media_Queries/Using_media_queries
          3. 逻辑操作符： not 、and、only、，
   
       2. 液态网格
   
          现代的方式是采用flex、grid、多列布局
   
       3. 液态图像
   
          1. 更好的响应式图片
   
          ```html
          <picture>
              <source type="MIME类型" srcset="*.png 400w(实际宽度)" sizes="(min-width: 500px) 400px">
              ...
              <img src="*.png" alt=""></img>
          </picture>
          ```
   
          2. 采用max-width: 100%;
   
       
   
   
   
   13. CSS是如何工作的
   
       https://developer.mozilla.org/zh-CN/docs/Learn/CSS/CSS_layout/Responsive_Design
   
   14. BFC
   
       1. BFC是块级元素布局过程的区域，也是浮动元素与其他元素交互的区域
       2. 创建BFC的方法
          1. overflow: hidden、auto;等 
          2. display: flow-root;
          3. 
   
   