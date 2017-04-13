## 模块定义
前端JS采用seajs进行模块化加载，关于seajs更多信息请参照：<http://seajs.org/docs/>
#### 模块定义的几种方法

    define(id?, deps?, factory) // define可以接受两个以上参数。字符串 id 表示模块标识，数组 deps 是模块依赖。

##### 1.标准模块定义
    define('hello', ['zepto'], function(require, exports, module) {

      //获取其他模块接口
      var a = require('./a');

      //定义模块代码
      var hello = {

      }

      //对外提供接口
      module.exports = hello;

    });

##### 2.使用 require 获取其他模块提供的接口
    define(function(require, exports) {

      //获取模块 a 的接口
      var a = require('./a');
      //调用模块 a 的方法
      a.doSomething();

    });

##### 3.使用 exports 对外提供接口
    define(function(require, exports) {

      //对外提供 foo 属性
      exports.foo = 'bar';

      //对外提供 doSomething 方法
      exports.doSomething = function(){

      };

    });
##### 4.也可通过 return 直接提供接口
    define(function(require) {

      //通过 return 直接提供接口
      return {
        foo: 'bar',
        doSomething: function() {}
      };

    });

## 模块编码风格约定
模块划分可根据业务模块，如订单(order)，购物车(cart)，用户(user)……
#### 模块中的 init() 方法
init()方法用于模块初始化，如进行：参数传入，事件绑定，变量赋值等操作。  
在不接受页面参数传入的情况下，init()方法可以写成自执行函数，如：
    
    define(function(require, exports) {

      init: function(){
        dosometing……
      }(),
    });
    
这样在页面加载后，init()方法会自动执行。
另外也可以模块对外提供接口前执行init()方法，如：

    define('hello', function(require, exports) {

      init: function(){
        dosometing……
      },

      hello.init();
      module.exports = hello;
    });

#### 模块中的方法封装
尽量将单一业务逻辑封装成function或对象的形式，做到业务粒度划分清晰，避免在一个对象中实现过多业务逻辑，降低模块内部对象之间的耦合。一个购物车模块的例子如下：

    define('cart', function(require, exports, module) {

      //定义模块代码
      var cart = {
        /*添加购物车*/
        add: function(){

        },
        /*修改购物车*/
        update: function(){

        },
        /*删除购物车商品*/
        remove: function(){

        },
        /*清空购物车*/
        clear: function(){

        },
        /*购物车初始化*/
        init: function(){

        }()
      }

      //对外提供接口
      module.exports = cart;

    });
