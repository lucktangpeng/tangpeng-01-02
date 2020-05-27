简答题

1. ​		描述引用计数的工作原理和优缺点

   1. 引用计数的工作原理是监听对象的引用计数，对象在被引用的时候计数会增加，对象在被取消引用的时候计数会减少，如果引用计数为零时就对为零的对象进行空间的回收。
   2. 优点
      1. 在对象为零的时候就即时进行对象回收，不需要等待
      2. 减少程序卡顿的时间
   3. 缺点
      1. 无法回收循环引用的对象
      2. 资源消耗大，因为要频繁的改变计数的值、

2. 描述标记整理算法的工作流程

   1. 标记整理算法的工作流程，主要分为两部分
      1. 第一部分循环遍历对象，找到活动对象，并做上对应的标记
      2. 第二部分循环遍历对象，清除没有标记的对象，在清理完没有标记的对象后，会把第一阶段做的标记都抹掉，以便于下次重新标记
      3. 回收的空间，会放入空闲列表中，以便于下次程序直接在空闲列表中申请空间进行使用。

3. 描述V8中心神带存储区垃圾回收的流程

   1. 新生代存储区分为From和To两个等大的空间，From为使用空间，To为空闲空间，活动对象一般都存储于From空间内，经过一个时间周期会对From中的活动对象进行标记整理后将活动对象拷贝到To中，然后释放From中的空间，释放完成后，将From和To的空间进行交换，将活动对象重新放入From中

4. 描述增量标记算法再何时使用及工作原理

   1. 增量式标记算法，适合那些相对更重视缩短最大暂停时间而不是最大吞吐量的应用程序
   2. 工作原理: 
      1. 增量标记算法的思想就是相当于把标记的对象分为多个小块，穿插在程序的执行过程中运行，因为小块内容不会太多所以程序暂停时间都是很小的，在这种模式下增量算法会给对象添加对应的颜色，分别是白色，灰色和黑色，在最开始的时候所有对象都是白色，在检查后对象会被变成黑色，已经在检查列表中但是还未被检查到的会被标记成灰色，当所有灰色都变成黑色的时候，代表此次标记结束了，此时仍然是白色的对象会被回收，回收结束这一轮标记就结束了

5. 练习1

   1. 使用函数组合fp.flowRight()重新实现下面的这个函数

   2. ```javascript
      class funtor {
        static of(val) {
          return new funtor(val);
        }
        constructor(value) {
          this._value = value;
        }
        map(fn) {
          return funtor.of(fn(this._value));
        }
      }
      
      const L = funtor.of(cars);
      
      console.log(
        L.map(function (val) {
          return fp.flowRight([fp.prop("in_stock"), fp.last])(val);
        })
      );
      ```

6. 练习2 

   1. 使用 fp.flowRight(), fp.prop()和fp.first()获取第一个car的name

      ```javascript
      class funtor {
        static of(val) {
          return new funtor(val);
        }
        constructor(value) {
          this._value = value;
        }
        map(fn) {
          return funtor.of(fn(this._value));
        }
      }
      
      const L = funtor.of(cars);
      
      console.log(
        L.map(function (val) {
          return fp.flowRight([fp.prop("name"), fp.first])(val);
        })
      );
      ```

7. 练习3

   1. 使用帮助函数_average重构averageDollarValue,使用函数组合的方式实现

      ```javascript
      let _average = function (xs) {
        return fp.reduce(fp.add, 0, xs) / xs.length;
      };
      let averageDollarValue = (cars) => {
        return fp.flowRight(
          _average,
          fp.map((car) => car.dollar_value)
        )(cars);
      };
      console.log(averageDollarValue(cars));
      ```

8. 练习4

   1. 使用flowRight写一个sanitizeNames()函数

      ```javascript
      
      let _underscore = fp.replace(/\W+/g, "_");
      function sanitizeNames(array) {
        return fp.flowRight(
          fp.castArray,
          _underscore,
          fp.lowerCase,
          fp.split(" ")
        )(array);
      }
      
      console.log(sanitizeNames(["Hello World"]));
      ```

9. 代码题2

   1. 练习1

      1. 使用fp.add(x,y)和fp.map(f,x)创建一个能让functor里的值增加的函数exl

         ```javascript
         let maybe = Maybe.of([5, 6, 1]);
         let exl = maybe
                   .map((x) => {
                     return fp.map(fp.add(1), x);
                   });
         console.log(exl);
         ```

   2. 练习2

      1. 实现一个函数ex2, 能够使用fp.first获取列表的第一个元素

         ```javascript
         let xs = Container.of(["do", "ray", "me", "fa", "so", "la", "ti", "do"]);
         let ex2 = xs.map((x) => {
           return fp.first(x);
         });
         console.log(ex2);
         ```

   3. 练习3

      1. 实现ex3,使用safeProp和fp.first找到user的名字的首字母

         ```javascript
         let safeProp = fp.curry(function (x, o) {
           return Maybe.of(o[x]);
         });
         let user = { id: 2, name: "Albert" };
         let ex3 = safeProp("name", user).map((x) => fp.first(x));
         console.log(ex3);
         ```

   4. 练习4

      1. 使用Maybe重写ex4,不要有if语句

         ```
         const n = "5";
         let maybe = Maybe.of(n).map((x) => parseInt(n));
         console.log(maybe);
         ```

         

