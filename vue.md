# vue

1. diff 

   对新旧vNode进行对比。同一父元素的同层元素进行对比。对比过程如下：

   1. 同层相同元素，不需要移动
   2. 同层相同元素，需要移动
   3. 同层不同元素，进行增加删除

2. 双向数据绑定

3. Vue组件之间参数传递

   1. 父组件和子组件传值

      1. props方法(父组件)
      2. $emit方法

   2. 子组件之间传值

      eventBus

4. Vue的生命周期
   1. beforeCreate
   2. creat
   3. beforemount
   4. mounted
   
5. mixin

   1. data中的数据app中优先，钩子函数被放在列表中，mixin的放在前面，值为对象的选项合并的时候相同属性取组件的属性

6. 自定义指令

   directives

## 面试题

1. Vue的优缺点。

   优点： 渐进式、组件化的、单页面的、响应式的、数据和页面分开的

   缺点：不利于seo(预渲染、服务器渲染)，不支持IE8以下的版本(defineproperty、promise)、首屏加载时间长（vue会把所有js、css合并成一个vendor.js的文件，如果包含了很多库的话，vendor就会很大，增大了浏览器加载js的时间）

2. MVVM和MVC的区别

   MVC的逻辑是model负责从数据库中拉取数据，view负责在前端显示，control负责把数据添加到view中

   MVVM的逻辑是model和view分开，通过viewmodel来实现数据的双向绑定。

3. data为什么是函数

   因为一个组件可能在很多地方被引用，如果是函数，那么引用的不同地方都能返回一个新的对象，不会造成数据污染

4. Vue修饰符
   1. lazy：表单光标离开时，才会改变数据
   2. trim：把v-model绑定的数据前后的空格去掉
   3. number：将输入的数据转化成数字
   4. .left 、right、middle：对应鼠标的左中右
   5. stop：停止冒泡
   6. capture：事件转化为捕获
   7. self：点击事件是自己的时候
   8. prevent：阻止默认事件
   9. passive：onscroll事件在移动端浏览器会产生卡顿，加上这个修饰符相当于加上了lazy
   
5. Vue内部指令
   1. v-show
   2. v-if、v-else-if、v-else
   3. v-for
   4. v-slot
   5. v-model
   6. v-bind
   7. v-on
   8. v-once
   
6. 组件传值有哪些方式
   1. 父子：props、emit、provide/inject
   2. VueX

7. 有几种路由模式

   1. hash：location接口上的hash会返回USVstring，包括URL后面的#和后面的标识符，hash字段有以下特点：
      1. #和后面的任何字符都不会发送到后端
      2. #后边的字符改变只会滚到相应的位置但是不会重新加载页面，改变之后，就会在浏览记录后面添加一次机会，点击退回可以返回上一个位置
      3. 可以通过window.location.hash来访问，也可以通过window.addEventListener('hashchange',fun)来监听变化
   2. history：通过pushState()、replaceState() 切换url，触发popState事件实现url切换，需要服务器配合。
   3. abstract：

8. 动态设置class和style

   通过对象、数组

9. v-if和v-show的区别

   v-if:通过对dom元素进行生成和删除实现的

   v-show:通过改变css来实现元素的显隐的

   经常需要改变的元素采用v-show，否则使用v-if

10. computed 和watch有什么区别

    1. computed是通过已有变量计算目标变量，经常是多个变量合成一个变量，他支持缓存，不支持异步
    2. watch是一个变量发生变化的时候去执行回调函数，支持异步

11. 生命周期

    1. beforeCreate: 创建了Vue实例，但是还没有进行初始化和响应式处理
    2. created：数据初始化和响应式处理完成，可以引用修改数据
    3. beforeMount：render在这里调用，生成了虚拟dom树，但是还没有挂载到el上
    4. mounted：已经挂载到el上
    5. beforeUpdate: 修改了虚拟dom树，但是还没有和旧虚拟dom树对比和打补丁
    6. update：修改到dom树上
    7. beforeDestrory：实例销毁之前调用，还可以访问到数据
    8. destroryed：实例销毁后调用 

12. v-if和v-for不能一起使用？

    在vue3中，v-if的优先级高于v-for，所以可能引用不到变量，在Vue2中，v-for比v-if有更高优先级，所以可能会导致不必要dom元素创建和删除

13. vuex是什么？有哪些属性和用处？

    vuex是单一的状态树，一个对象包含了全部的应用层级状态。能够让我们直接定位任意特定的状态片段

    state：定义了应用状态的数据结构，可以设置默认的初始值

    getters：允许从store中获取数据，并且也可以绑定一些操作

    mutation：唯一改变store中状态的方法，必须是同步函数

    action：用于提交mutation，可以包含任意异步函数

    module：单一的store分解为多个store，保存在状态树中
    
    ```javascript
    const store = new Vuex.Store({
    	state:{
    		count: 1,
    	},
        getters:{
            getCount:function(){
                return state.count + 1;
            }
        }
    })
    
    const app = Vue.createApp({
    	d                          
    })
    ```

14. 不需要响应式的数据
    1. 放在data外面定义
    2. Object.freeze

15. watch有哪些属性，有什么用
    1. deep:可以深度检测对象中的每一个属性，
    2. immediate:立刻执行handler函数

16. 父子组件生命周期顺序
    1. 父beforeCreate、父created、父beforeMount、子beforeCreate、子Created、子beforeMount、子Mounted、父Mounted

17. 什么是nextTick
    1. 将回调函数放在下一次更新dom的时候调用

