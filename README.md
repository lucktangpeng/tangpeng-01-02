# 简答题

1. 最终执行结果是10，因为for循环是使用var定义的i,var定义的i是不受块作用域限制的，所以在for循环执行过程中是没有问题，等到consoloe.log()打印的时候，会在局部找i变量，然后向上查找i，因为var定义的i不受块级作用域限制，所以concoloe原本的i值都被，全局i覆盖了，所以全部打印出10

2. 执行结果就是报错，因为let定义的时候会形成暂时性死区，在这个块级作用域内，使用let声明之前，该变量是不可用的

3. Math.min(...arr)

4. 

   1. var
      1. var 会有变量提升，可以在变量定义之前引用变量，只不过值是undefined
      2. 不被块级作用域限制，可以上升为全局变量
   2. let
      1. let 使用时会有暂时性死区，在块级作用域内使用let定义变量之前，不能引用该变量
      2. 去除了变量提升的特性，规定调用前一定要先定义
      3. 定义的变量只在，块级作用域内有效
   3. const
      1. 是一个常量，比let多了一个只读特性
      2. 声明后不可修改，这个不允许修改，只针对于存储地址的修改

5. 结果是20， 因为settimeout是箭头函数，所以this的指向就是调用fn函数的对象，执行的时候是obj调用的fn函数，所以打印obj里面a的数值20

6. Sym的主要用途一般用于一些常量和变量的定义或者拿来当作KEY值，用Symbol定义的变量和常量能够保证他们是唯一的，不会重复

7. 浅拷贝

   1. 浅拷贝的机制在对象中没有类似于对象和数组的时候，其实就是将里面的数据进行拷贝，然而如果里面又对象和数组之类的数据时，只会拷贝对象和数组的指针到新的对象内，新对象更改，旧对象也会受到影响

   深拷贝

   ​	深拷贝就是通过递归将拷贝对象里面的对象和数字这些数据，用递归的方式一层一层拷贝出来，完全分离开，保证新旧数据不受任何影响

8. JS异步编程是为了节省一些耗时任务的等待时间，先去做其他事通过回调来处理，就不会造成等待耗时任务造成的页面卡顿了，Event Loop相当于就是消息队列，队列中会分为微服务队列和宏服务队列用于管理他们之间的执行规则，宏服务代表的是主要代码任务内容，微服务相当于是主要代码分支出来的细节

9. ```javascript
   const L = new Promise((resolve, reject) => {
     setTimeout(function () {
       var a = "hello";
       resolve(a);
     }, 2);
   }).then((res) => {
     return new Promise((resolve, reject) => {
       setTimeout(function () {
         var b = "lagou";
         resolve(`${res} ${b}`);
       }, 2);
     }).then((res) => {
       return new Promise((resolve, reject) => {
         setTimeout(function () {
           var c = "I love u";
           resolve(`${res} ${c}`);
         }, 2);
       });
     });
   });
   
   L.then((res) => {
     console.log(res);
   });
   ```

10. Javascript 是一种轻量级的解释性脚本语言，一般用于html页面的开发

    Typescript 是javascript的超集，包含了javascript的所有元素，可以载入javascript的代码运行，并扩展了javascript的语法

    TypeScript 可以使用javaScript中额所有代码和编码概念，TypeScript是为了是javaScript的开发变得更加容易而创建的

    TypeScript的优势

    更好的协作，更强的生产力，更快捷的项目重构，代码质量更好，更清晰

11. 

    1. TypeScript的优点
       1. 有更好的代码错误检查，更健全的代码规范
       2. 编写的代码更加健壮，使得代码质量更好更清晰
       3. 使用typescript工具来重构变得更加容易和快捷
       4. 干净的 ECMAScript 6 代码，自动完成和动态输入等因素有助于提高开发人员的工作效率
    2. TypeScript的缺点
       1. 学习成本提高，需要理解接口，泛型，类，枚举等新的概念
       2. 短期可能会怎加一些开发成本，笔记要多写一些类型的定义
       3. 集成到构建流程需要些工作量
       4. 可能和一些库结合的不是很完美



