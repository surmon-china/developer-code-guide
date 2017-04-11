## JavaScript编码规范&语风规范

### 变量/对象/数据处理

-  创建普通对象时仅使用字面量（直接量）方式创建，例：

        // bad code
        var obj = new Object();
        var arr = new Array();

        // good code
        var obj = {};
        var arr = [];


- 每个 var 只能声明一个变量，一个 var 声明多个变量，容易导致较长的行长度，并且在修改时容易造成逗号和分号的混淆，例：

        // bad code
        var a = '',
            b = [],
            c = {};

        // good code
        var a = '';
        var b = [];
        var c = {}; 


*** 

### 方法/函数/程序设计

  * 任何一个函数的参数若超过2个，则使用对象来传递，例：

        // bad code
        var fun = function(a, b, c) {
          console.log(a + b + c);
        }

        // good code
        var fun = function(params) {
          console.log(params.a + params.b + params.c);
        }



* 方法链式调用时，无论代码量，务必要保持代码缩进结构清晰一致，例：

        // bad code
        var a = require('a');
        a.get('b').del('c').put('d').post('e')

  
        // good code 
        var a = require('a');
        a 
        .get('b')
        .del('c')
        .put('d')
        .post('e');


* 不允许修改和扩展任何原生对象和宿主对象的原型，例：
  
        // bad code
        String.prototype.trim = function() {
        };
  

* 属性在构造函数中声明，方法在原型中声明；原型对象的成员被所有实例共享，能节约内存占用；所以编码时我们应该遵守这样的原则：原型对象包含程序不会修改的成员，如方法函数或配置项。


* 设计自定义事件时，应考虑禁止默认行为，常见禁止默认行为的方式有两种：

      - 事件监听函数中 return false
      - 事件对象中包含禁止默认行为的方法，如 preventDefault

***

### 逻辑/技巧相关

* 非特定场景下，尽量使用for循环代替while


* 逻辑分支超过5种的判断，使用switch case，switch case需要带default


* 在逻辑计算中，优先级： "||"  >  三目运算( ? : )  >  if else ，按需使用


* 一段if条件中 "&&" or "||" 条件超过3个以上，则按照以下两种方式处理，以保证代码易读性与可维护性

      -  根据逻辑条件合理缩进换行

      -  在if语句前将判断句存储为变量， 例：

        // bad code
      
        if(a == 0 || ( b == 1 && c == 2 ) || d == 3) {  do something...  } 

      
        // good code 
    
        // 存储变量处理
        var is_dsiplay  = a == 0;
        var is_valid    = b == 0 && c == 2;
        var is_read     = d == 3;
    
        if(is_dsiplay || is_valid || is_read) {  do something...  } 
    
        // 缩进换行处理
        if(a == 0 
          || ( b == 1 && c == 2 ) 
          || d == 3
        ){
          do something...  
        }


*  在JS代码中进行Dom拼接时，如果Dom字节很多，应按一定长度截断字符串，并使用 + 运算符进行连接，分隔字符串尽量按语义进行，如：不要在一个完整的名词中间断开，特别对于 HTML 片段的拼接，可以通过缩进保持和 HTML 相同的结构，例：
  
    下文中假设dom字节过多
   
        <!-- bad code -->
        var dom = '<div><span><i>Hello!</i></span></div>';

  
         <!-- good code -->
        var dom = '<div>'+
                  '<span>'+
                    '<i>Hello!</i>'+
                  '</span>'+
                  '</div>';

        <!-- 此处用一个空字符串，以便整个 HTML 片段都在新行严格对齐 -->
        var dom = ''
                + '<article>'
                +     '<h1>Title here</h1>'
                +     '<p>This is a paragraph</p>'
                +     '<footer>Complete</footer>'
                + '</article>';


## 编写规范

### 注释规范

* js文件、模块，起始部分使用 “ /* ... */ ” 注释文件、模块的基本信息，例：

        /**
        * AsideController Module
        * @author      surmon#foxmail.com
        * @data        2016-03-01
        * @Description 边栏控制器模块的说明...
        */
  

* 在文件中 关于程序的内的信息使用双斜线 " // " 单行注释，避免使用 /* ... */ 这样的多行注释。有多行注释内容时，使用多个单行注释，例：

        // 获取文章
        var getPost = function () { 
               // 如果...
               if () {}
         }
  

### 符号规范

* if / else / for / while / function（匿名） / switch / do / try / catch / finally 关键字后，必须有一个空格，例：
    
        // bad code
        if(condition) {
        };

        while(condition) {
        };

        (function() {
        })();
  

        // good code
        if (condition) {
        };

        while (condition) {
        };

        (function () {
        })();


* 在对象创建时，属性中的 " : " 之后必须有空格， " : " 之前不允许有空格，例：
  
        // bad code
        var obj = {
             a : 1,
             b:2,
             c :3
        };

        // good code 
        var obj = {
             a: 1,
             b: 2,
             c: 3
        };


* 函数声明、具名函数表达式、函数调用中，函数名和 " ( " 之间不允许有空格，例：

        // bad code
        function funcName () {
        };

        var funcName = function funcName () {
        };

        funcName ();
  
  
        // good code 
        function funcName() {
        };

        var funcName = function funcName() {
        };

        funcName();


*  " , " 和 " ; " 前不允许有空格，如果不位于行尾 " , " 和 " ; " 后必须跟一个空格，例：

        // bad code 
        callFunc(a , b) ;
  
        // good code
        callFunc(a, b);   
  
### 逻辑规范

* 适当环境下，尽可能使用简洁的表达式，例：

        // bad code
        if(a == '' || a == undefined || a == 0) {
            do something...
        }
  
        // good code
        if(!a) {     // 转换为布尔值，且取反值
            do something...
        }


* 判断条件中，对条件进行简洁的转换，例：

        // bad code
        if(a) {
            do something...
        }
  
        // good code
        if(!!a) {     // 将结果转换为布尔值
            do something...
        }
  

* 避免在循环体、定时器、中包含函数表达式，遵循迪米特法则，将任何一个元素都看做一个独立的对象

        // bad code 
        for(...) {
            // function() { ... }
        }
  
        // good code
        var fun = function() { ... };
        setTimeout(fun, 1000);
        for(...) {
            fun();    
        };

> [参考文献1（guide - JavaScript编码规范）](https://github.com/surmon-china/spec/blob/master/javascript-style-guide.md)

> [参考文献2（guide - ES6编码规范）](https://github.com/surmon-china/spec/blob/master/es-next-style-guide.md)