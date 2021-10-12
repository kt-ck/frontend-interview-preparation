# JS

1. 头等函数

   函数可以当做变量来传参、返回、赋值

2. 原型编程

   面向对象编程的一种风格，这种风格不会显式的定义类，而是通过给对象添加属性和方法来创建类，甚至可以采用空对象创建类

3. 修饰

   1. async 异步加载，用在js代码与html和其他js无关的情况
   2. defer 在页面解析完后，按顺序

4. 扩展原型链的方法

   1. 通过new方法创建对象，设置prototype

   2. 通过Object.create([原型对象], {property:{value: }})函数创建对象，在设置prototype

   3. 通过Object.setPrototypeOf(obj, prototype)函数给已经存在的对象修改原型对象， 在设置prototype

      *这个函数有返回值为添加原型对象后的对象。

      这个方法表现不好，动态设置原型干扰了浏览器的优化，

   4. 创建对象采用

      ```javascript
      {
        property: value,
        __proto__:{
          ....
        }
      }
      ```

      *表现不好，理由和3一样

5. 字面量

   1. 数组字面量
   2. 布尔字面量
   3. 整数字面量
   4. 浮点数字面量
   5. 字符串字面量（模板字符串）
   6. 对象字面量：属性值得字面量可以使字符串也可以是数字或者是标识符
   7. 正则字面量

6. 闭包

   1. 定义在内部的函数可以访问外部函数所有的参数和函数，包括外部函数能访问的参数和变量。
   2. 当内部函数生存周期大于外部函数的时候，内部函数访问的变量会和内部函数绑定在一起，只有通过内部函数才能访问。

7. 函数

   1. 参数

      1. arguments类数组获得参数列表
      2. 可以设置默认参数
      3. 剩余参数语法为 ...args ，args是数组

   2. 绑定函数

      1. 将函数的this绑定到特定的对象上,以至于不需要每次都调用call函数并指定对象。

         ```
         let obj = {
           x: 2,
           getX: function(){
            return this.x;
           }
         }
         
         let getXfunc = obj.getX;
         getXfunc.bind(obj);
         getXfunc(); //return 2
         ```

      2. 绑定固定的参数
      3. 配合window.setTimeout(this.function.bind(this), 1000);

8. 继承

   1. 通过原型链

      1. 缺点：
         1. 引用类型数据被所有子类共享
         2. 创建子类的时候不能向超类的构造函数中传递参数

   2. 通过class

      1. 类声明不会被提前
      2. 

   3. 通过借用构造函数

      call([obj], args...)

      缺点：

      	1. 不能复用函数
      	2. 不能复用父类原型上的属性

      ```javascript
      function Parent(name, age){
          this.name = name;
          this.age = age;
      }
      
      function Child(name, age, sex){
          Parent.call(this, name, age);
          this.sex = sex;
      }
      ```

   4. 组合继承

      两次调用父类的构造函数

   5. 原型式继承

      Object.create(prototype, {property:{value: ""}})

      缺点：引用型数据会共享值

   6. 寄生式继承

      在函数中调用create函数，然后再添加属性，最后返回对象

      无法实现函数复用

   7. 寄生组合式

      ```javascript
      function Person(name){
          this.name = name;
      }
      
      Person.prototype.greeting = function(){
          console.log(this.name);
      }
      
      function Student(id,name){
          Person.call(this, name);
          this.id = id;
      }
      
      Student.prototype = Object.create(Person.prototype);
      Student.prototype.constructor = Student;
      ```

      

9. Data 

   1. Data() 仅返回当前日期(string)，不受参数影响;new Date()返回对象，拥有很多方法

   2. 参数

      1. 空参数
      2. 字符串：月 日,年 时：分：秒
      3. 参数列表：年月日[时分秒]

   3. 函数

      1. getTime() 获得毫秒数
      2. getMonth() 获得月份 0-11
      3.  getDay() 获得星期
      4. getFullYear()
      5. getHours()
      6. getMinutes()
      7. getSeconds()

      5. Date.parse(string) 返回毫秒数

   10. 正则表达式

       1. *: 0 个 或者多个 {0,}
       2. +：{1, }
       3. ?: {0, 1} 当用在量词后面，则采用非贪婪的方式
       4. ^: 开始
       5. $: 结束
       6. . :除了换行符以外的单个字符
       7. x(?=y) ：匹配仅当x后面跟着y的x
       8. (?<=y)x: 匹配x前面是y的x
       9. x(?!y): 不跟着y的x
       10. (?<!y)x: x前面没有y 

       11. [^x-y]: 不包含x-y

       12. [].filter(t=>/.../.test(t))

       13. //.exec('') 返回匹配的字符串 和index

       14. string.match(/.../)

   11. Array

       1. forEach(function(){})

       2. concat(arg1,arg2..) 返回增加后的数组

       3. join("-")

       4. push(arg1,arg2) 在原数组上添加，返回数组长度[在原函数上]

       5. pop() 从数组的最后删除元素，返回弹出的元素[在原函数上]

       6. shift() 移除数组的第一个，返回该元素[在原函数上]

       7. unshift(arg1, arg2) 从头添加一个或者多个[在原函数上]

       8. splice(index, num, ...args)[在原函数上]

       9. slice(begin, end) 

       10. sort(func) [在原函数]

       11. indexOf(elem, begin) 从begin以后第一次出现elem的下标

       12. lastIndexOf(elem, from) 从end开始

       13. map(func, thisobj) 返回值覆盖原元素[在原函数上]

       14. every(func, thisobj) func返回bool，判断每个元素是否都满足func

       15. some(func, thisobj) 只要有一个

       16. filter(func, thisobj) 返回为true的所有元素

       17. reduce(callback, initialvalue), 两两执行操作

           ```javascript
           //1. 判断this是否为null、 callback是否为function
           //2. 获得长度值 >>> 0
           //3. 初始化value
           //4. 逐个计算，返回最终结果
           
           if(!Array.prototype.reduce){
               Object.defineProperty(Array.prototype, 'reduce',{
                   value: function(callback/*,initial*/){
                       if(this === null){
                           throw new TypeError("reduce is called on null or undefined");
                       }
                       
                       if(typeof callback !== "function"){
                           throw new TypeError("callback is not function");
                       }
                       
                       let obj = Object(this);
                       
                       let length = obj.length >>> 0;
                       let value;
                       let index = 0;
                       if(arguments.length >= 2){
                           value = arguments[1];
                       }else{
                           while( index < length && !(index in obj)){
                               ++index;
                           }
                           
                           if(index >= length){
                               throw new TypeError("Empty Array");
                           }
                           value = obj[index++];
                       }
                       
                       while(index < length){
                           if(index in obj){
                               value = callback(value,obj[index], index, obj);
                           }
                           ++index;
                       }
                       
                       return value;
                   }
               })
           }
           ```

           

       18. reduceRight(callback, initialvalue),从右到左

       19. 可以采用Array.prototype.forEach.call(arguments, function(args){})

   12. Map

       1. set('', '') 、get('')、size、has('')、delete('')、clear()
       2. Object 和Map的比较
          1. Object的所有键都是string、Map的键是任意的
          2. Object的size需要手动计算、Map不需要
          3. Map的遍历顺序就是插入的顺序
          4. object有原型所以有缺省的键

   7. 对象

      1. Object.getOwnPropertyNames(o),返回所有属性，包括非枚举属性（不包括原型链上的属性）

      2. Object.keys(o) 返回所有枚举属性（不包括原型链上的属性）

      3. for..in 访问所有枚举属性（包括原型链上的）

      4. get、set

         ```
         {
          get func(){
          
          },
          
         }
         ```

      5. Object.defineproperties(obj, {

           "name": {

            	get: function() {},

         ​      set: function(){}

            }

         })

      6. Promise

           1. promise是一个对象，用来表示异步操作的成功或者失败，他可以解决函数调用地狱的问题，在异步操作之后返回promise对象，在这个对象上绑定回调函数

           2. 3种状态：待定、已兑现、已拒绝

           3. 已决议状态：任何不是通过throw终止，创建已决议状态

              已拒绝状态： 通过throw终止，创建已拒绝状态

           4. Promise.All(iterableObj)

              1. 当iterableObj为空，返回resolved的promise
              2. 当iterable中不包含promise对象，则返回异步完成的promise对象
              3. 否则当所有promise都完成后，返回已完成，返回所有成功结束promise的数据数组，或者有一个被拒绝，返回被拒绝promise

           5. Promise.race(iterableObj)

              1. 一旦有一个promise对象判定结果，就直接返回相应的promise对象

              ```javascript
              //define three status
              const Panding = "panding";
              const Fulfilled = "fulfilled";
              const Rejected = "rejected";
              //define Promise
              function Promise(executor){
                  // define property
                  let self = this
                  let state = Panding;
                  let onFulfilled = [];
                  let onRejected = [];
                  //define resolve function
                  function resolve(value){
                      if(self.state === Panding){
                          self.state = Fulfilled;
                          self.value = value;
                          self.onFullfilled.forEach(fn=>fn());
                      }
                  }
                  //define reject function
                  function reject(reason){
                      if(self.state === Panding){
                          self.state = Rejected;
                          self.reason = reason;
                          self.onRejected.forEach(fn=>fn());
                      }
                  }
                  //exec executor
                  try{
                      executor(resolve, reject);
                  }catch(e){
                      reject(e);
                  }
              }
              
              //define then function
              Promise.prototype.then = function (onFulfilled, onRejected){
                  //prepare resolve and reject function
                  onFulfilled = typeof onFulfilled === "function" ? onFulfilled: onFulfilled=>onFulfilled;
                  onRejected = typeof onRejected === "function" ? onRejected: onRejected=>onRejected;
                  
                  let self = this;
                  //new Promise, call suitable function
                  let promise2 = new Promise(function(resolve, reject){
                      if(self.state === Fulfilled){    
                        settimeout(()=>{
                          try{
                              let x = onFulfilled(self.value);
                              resolvePromise(promise2, x, resolve, reject);
                          }catch(e){
                              reject(e);
                          }
                        });
                      }else if(self.state === Rejected){
                        settimeout(()=>{
                          try{
                              let x = onRejected(self.reason);
                              resolvePromise(promise2, x, resolve, reject);
                          }catch(e){
                              reject(e);
                          }
                        });
                      }else if(self.state === Panding){
                          self.onFulfilled.push(()=>{
                              settimeout(()=>{
                                  try{
                                      let x = onFulfilled(self.value);
                                      resolvePromise(promise2, x, resolve, reject);
                                  }catch(e){
                                      reject(e);
                                  }
                              });
                          });
                          
                          self.onRejected.push(()=>{
                              settimeout(()=>{
                                  try{
                                      let x = onRejected(self.reason);
                                      resolvePromise(promise2, x, resolve, reject);
                                  }catch(e){
                                      reject(e);
                                  }
                          })
                      }
                  })
                  //return Promise
                  return promise2;
              }
              //define resolvePromise Function
              function resolvePromise(promise2, x, resolve, reject){
                  let self = this;
                  if(promise2 === x){
                      reject("chaining circle");
                  }
                  
                  if(x&& typeof x === "object" || typeof x === "function"){
                      let used;
                      try{
                          let then = x.then
                          if(typeof then === "function"){
                              then.call(x, (t)=>{
                                  if(used) return;
                                  used = true;
                                  resolvePromise(promise2, y, resolve, reject);
                              }, (e)=>{
                                  if(used) return;
                                  used = true;
                                  reject(e);
                              })
                          }else{
                              if(used) return;
                              used = true;
                              resolve(x);
                          }
                      }catch(e){
                          if(used) return;
                          used = true;
                          reject(e);
                      }
                  }else{
                      resolve(x);
                  }
              }
              //export module
              module.exports = Promise;
              ```

              ```javascript
              Promise.all = function(promises){
                  return new Promise(function(resolve, reject){
                      let result = []
                      if(promises.length === 0){
                          resolve(result);
                      }
                      let pending = promises.length;
                      
                      let callPromise = function(i){
                          promises[i].then(value=>{
                              result.push(value);
                              if(!--pending){
                                  resolve(result);
                              }
                          },reject);
                      }
                      
                      let i = promise.length;
                      while(i--){
                          callPromise(i);
                      }
                      
                  })
              }
              
              Promise.race = function(promises){
                  
                  return new Promise(function(resolve, reject){
                      promises.forEach(promise=>{
                          promise.then(resolve, reject);
                      })
                   })
              }
              ```
              
              

      15. async/await

          1. ```javascript
             async function(){
                 try{
                     let value = await promise;
                 }catch(errorValue){
                     
                 }
             }
             ```

      16. AJAX

          1. httpRequest 不能在全局作用域使用，他会在makeRequest()函数中被覆盖从而导致资源覆盖

          2. ```
             (function(){
             	let httpRequest = new XMLHttpRequest();
             	httpRequest.onreadystatechange = func;
             	http.open('GET','url');
             	httpRequest.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
             	http.send("");
             	function func(){
             	  try{
             	   if(httpRequest.readyState === XMLHttpRequest.DONE){
             	   	 if(httpRequest.state === 200){
             	   	 	alert(httpRequest.responseText);
             	   	 }else{
             	   	    alert("There was a problem");
             	   	 }
             	   }
             	   }catch(e){
             	     console.log(e.description);
             	   }
             	}
             })()
             ```

      17. 事件：

          鼠标事件（click、dbclick、mouseenter、mouseleave）

          键盘事件：（keypress、keydown、keyup）

          表单事件：focus、blur、change、submit

          window事件: load、resize、scroll、unload

      18. jquery

          1. 效果

             fadeIn（speed，callback）;

             fadeOut(speed, callback);

             fadeToggle(speed, callback);

             fadeTo(speed, opacity,callback);

              slidedown(speed,callback)

             slideUp(speed, callback)

             slideToggle(speed,callback)

             animate({param},speed,callback)// 多个animate可以逐个调用

             stop()// 停止效果和animate

          2. 操作html

             1. text() 、html()、val()

                没有参数那么为get，设置参数或者或者参数是callback，那么为set

                callback(index, old){

                   return new;

                }

             2. attr({keystr:valuestr});

                attr(keystr, callback); //callback(index, old){

                ​	return new;

                }

             3. 插入元素

                append(htmlstr，...); //在元素内部的尾部插入

                prepend(htmlstr, ....) // 在元素内部的首部插入

                before(htmlstr)

                after(htmlstr);

             4. 创建元素

                $("<text></text>").html("text");

                document.createElement("text").innerhtml = text;

             5. 删除元素

                1. remove(arg， ..) // 删除本元素和所有子元素(arg选择)
                2. empty() // 删除本元素内所有子元素

             6. 操作样式

                1. addClass("classname1 classname2")

                2. removeClass("classname")

                3. toggleClass("classname");

                4. css("cssproperty"); // get

                   css("cssproperty", "value");//set

                   css({"cssproperty": "value"});

             7. 元素宽高
                1. width()、innerWidth() 、outerWidth（）、outerWidth（true）

          3. 遍历dom树

             1. parent（）直系父元素 
             2. parents（arg）所有父元素，args是filter
             3. parentsUntil(arg) 
             4. children() 直系所有子元素
             5. find(”fiter“) 所有后代元素
             6. siblings('filter')
             7. next()
             8. nextAll('p');
             9. nextUntil('');
             10. first()、last()、eq(index),filter("选择器") 、not（"选择器"）

          4. AJAX

             1. $.get(url, function(data, status){

                

                })

             2. $post(url, param, functon(data, status))// status 可能是success也可能是error

      19. Vue

          1. 双向绑定的原理：采用数据劫持和发布订阅模式。数据劫持采用js中Object.defineProperty实现，将数据转化成getter和setter，在setter中通知订阅者

             在Complie中对每个节点中指令解析更具指令模板替换数据以及绑定函数

             watcher作为连接Watcher和Compile的桥梁，用于发布属性更新的通知，执行回调函数，更新视图。

          2. MVVM：核心部件是ViewModel，他对Model中的数据进行绑定，对VIew中的Dom进行监听。当Dom中的数据或者Model中的数据变化的时候能实时一起更改。从而达到数据的双向绑定

      20. 浏览器缓存机制：

          1. 缓存的位置

             1. Service Work。是浏览器背后独立运行的线程，由于需要拦截请求，用在https请求中。他和其他浏览器内置的缓存机制不同，可以规定缓存什么数据，如何匹配、如何获取。缓存的流程是：获得service对象，监听到install事件的时候，缓存文件，下次请求相同文件的时候，拦截请求，查看时候有匹配的文件，有的话就返回，没有的话就去按照优先级请求。
             2. Memory cache是内存中的缓存，当Tab标签页关闭的时候，缓存就会消失，这种缓存不会受到http缓存头cachecontrol的影响，缓存的时候除了考虑url，还考虑content-type、cors等
             3. disk cache。缓存在硬盘中，根据http缓存头来确定是否缓存、是否更新
             4. Push cache。存在于http2中，只在session中存在，会话结束就会被释放

          2. 缓存机制：强缓存优先于协商缓存。当强缓存生效的时候，采用强缓存，强缓存失效，使用协商缓存，由服务器决定是否使用缓存，协商缓存生效，返回304，使用缓存，失效返回200，并更新文件

             1. 强缓存：不会向浏览器发送请求，从缓存中请求文件

                1. 设置方法：
                   1. expires：需要和last-modified配合使用，值为max-age+服务器时间 。http1的产物。
                   2. cache-control：
                      1. public：允许代理和客户端缓存
                      2. private：只允许客户端缓存
                      3. max-age=30： 在一段时间内使用强缓存
                      4. s-max-age=30：覆盖max-age（只在代理服务器中生效）
                      5. max-stale=30：能够容忍最大的过期时间
                      6. min-fresh=30： 时间内希望获得最新响应
                      7. no-store：不缓存
                      8. no-cache：缓存但是立刻过期，下一次请求的时候需要请求服务器是否使用缓存，也就是协商缓存（Etag、lastModified）

             2. 协商缓存：强缓存失效后，浏览器携带缓存标识向服务器发送请求。协商生效返回304、Not Modified，协商成功返回200和请求结果

                1. 实现：

                   1. last-Modified和last-modified-since。

                      弊端：如何只是读文件，还是会造成last-Modified被修改，服务器不能命中导致重新发送资源，如果在1s内修改了文件，不会反应在last-modified上，导致不会重新发送文件

                   2. Eag 和 if-not-match

      21. 关于cookie和session机制

          1. cookie如果设置了过期时间，那么缓存在硬盘上，没有设置过期时间，缓存在内存上
          2. session拥有唯一的sessionid，通过cookie或者编码在url中传递给浏览器
          3. 区别：
             1. session存在服务器、cookie存在客服端
             2. cookie存储文件的大小有限制
             3. cookie只能保存文本，session可以保存任意类型的数据，结构是HashTable

      22. localStorage和SessionStorage

          1. localStorage保存在本地，除非人为删除，否则不会删除
          2. SessionStorage存在于一次会话中，只要浏览器页面没有关闭，刷新页面或者同源的不同页面数据存在。
          3. 他们的大小一般只有5MB，只存文本类型不和客户端交互

      23. 事件冒泡和捕获

          1. 默认是冒泡，通过stopPropagation()停止
          
      16. CORS

            1. 简单请求：不会引起CORS预检请求的请求

                 满足5个条件：

                 1. get、post、head中的一个
                 2. 人为定义的字段需要是fetch规范定义的对CORS安全的字段（Accept、Content-language、Accept-language）
                 3. content-type：text/plain、multipart/form-data、application/x-www-form-urlencoding
                 4. 请求中没有readableStream对象

            2. Options预检请求

            3. 请求头：Access-Control-request-method、access-control-request-header、origin

                 响应头：Access-control-allow-method、access-control-allow-header、access-control-allow-origin

      17. http

            1. http1.0和http1.1的区别
               1. 缓存
               2. 24个错误状态码
               3. 有效利用带宽
               4. host头处理
               5. 长连接和请求流水线

            2. SPDY

               12年google发布了SPDY方案，优化了http1.x的延迟和安全性

               1. 采用多路复用技术。通过多个Steam共享一个tcp连接，解决线头阻塞问题，降低了延迟
               2. 设置优先级，优先级高的数据先传送
               3. header压缩
               4. https的安全传输
               5. 服务端推送

            3. http2

               1. 基于SPDY的，但是也有不同，比如头部压缩算法，http2支持明文传输，SPDY默认https传输

               2. 和http1的不同：多路复用，采用二进制，header压缩，服务端推送

      18. 防抖和节流

          ```javascript
          function fd(fn, seconds){
              let time;
              return function(){
                  if(time){
                      clearTimeout(time);
                  }
                  let self = this;
                  let args = arguments;
                  time = setTimeout(()=>{fn.apply(self, args)},seconds);
              }
          }
          
          function jl(fn, seconds){
              let time;
              return function(){
                  if(time){
                      return;
                  }
                  let self = this;
                  let args = arguments;
                  time = setTimeout(()=>{
                      fn.apply(self, args)}, seconds);
                      time = null;
              	}
          	}
          }
          ```

          

   19. ES6有哪些语法？
       1. let
       2. 对象键值简写
       3. 模板字符串
       4. 箭头函数
       5. promise
       6. class
       
   20. cookie
       1. name字段
       2. value字段
       3. domain字段
       4. Path字段
       5. SameSite字段 None、Strict、Lax

   21. CSRF

       1. 攻击者引用用户访问一个网站，那个网站向被攻击网站发送攻击内容，由于用户登陆过被攻击的网站，所以这次跨域请求带有cookie，这样可以绕过用户的验证。
       2. 防护策略
          1. 针对不明外域访问
             1. 同源检测（Origin、Refer）
             2. samesite Cookie
          2. CSRF token（保存在session中）
             1. token输出到页面中
             2. 请求的时候携带这个token

   22. XSS攻击

       1. HTML转义

       2. 设置白名单，禁止javescript：这种开头的链接

       3. 类型：存储型XSS攻击、反射型XSS攻击、DOM型XSS攻击

          1. 存储型和反射型的预防

             1. 纯前端渲染，把数据和代码分开，然后通过ajax加载用户数据，更新在页面上
             2. html转义

   12. 图片懒加载

       ```javascript
       
       function getLazyload(){
           let imgs = document.getElementsByTagName('img');
           let visualHight = window.innerHeight;
           let num = 0;
           return function(){
       		for(let i = num; i < imgs.length; ++i){
                   if(imgs[i].getBoundingClientRect().top < visualHight){
                       imgs[i].src = imgs[i].getAttribute('data-src');
                       ++num;
                   }
               }
           }
       }
       
       let lazyload = getLazyload();
       window.onload = lazyload;
       
       function debounce(fn, delay){
           let time=null;
           return function(){
               if(time){
                   clearTimeout(time);
               }
               let self = this;
               time = setTimeout(()=>{
                   fn.apply(self, arguments);
               }, delay);
           }
       }
       
       document.addEventListener('scroll', debounce(lazyload, 300), false);
       ```

       

       
