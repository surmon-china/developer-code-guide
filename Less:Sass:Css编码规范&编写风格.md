## Less/Sass/Css编码规范

### Css编码规范

#### 文件格式

- CSS 文件统一使用无 BOM 的 UTF-8 编码

#### 语符规范

- 选择器 与 " { "之间必须包含空格，例：

        .selector {
            margin: 0;
            padding: 0;
        }


-  属性名 与其之后的 : 之间不允许包含空格， : 与 属性值 之间必须包含空格，例：

        margin: 0;


-   列表型属性值 书写在单行时，, 后必须跟一个空格，例：

        font-family: Arial, sans-serif;

- 对于超长的样式，在样式值的 空格 处或 , 后换行，建议按逻辑分组，例：

        // 不同属性值按逻辑分组
        background:
            transparent url(aVeryVeryVeryLongUrlIsPlacedHere)
            no-repeat 0 0;

        // 可重复多次的属性，每次重复一行
        background-image:
            url(aVeryVeryVeryLongUrlIsPlacedHere)
            url(anotherVeryVeryVeryLongUrlIsPlacedHere);

        //类似函数的属性值可以根据函数调用的缩进进行
        background-image: -webkit-gradient(
            linear,
            left bottom,
            left top,
            color-stop(0.04, rgb(88,94,124)),
            color-stop(0.52, rgb(115,123,162))
        );

#### 核心顺序

-  > 同一 rule set 下的属性在书写时，应按功能进行分组，并以 Formatting Model（布局方式、位置） > Box Model（尺寸）  > Typographic（文本相关） > Visual（视觉效果） 的顺序书写，以提高代码的可读性。

    * Formatting Model 相关属性包括：position / top / right / bottom / left / float / display / overflow 等

    * Box Model 相关属性包括：border / margin / padding / width / height 等

    * Typographic 相关属性包括：font / line-height / text-align / word-wrap 等

    * Visual 相关属性包括：background / color / transition / list-style 等

    另外，如果包含 content 属性，应放在最前面。

    示例：

        .sidebar {
            // formatting model: positioning schemes / offsets / z-indexes / display / ...
            position: absolute;
            top: 50px;
            left: 0;
            overflow-x: hidden;

            // box model: sizes / margins / paddings / borders / ... 
            width: 200px;
            padding: 5px;
            border: 1px solid #ddd;

            // typographic: font / aligns / text styles / ...
            font-size: 14px;
            line-height: 20px;

            // visual: colors / shadows / gradients / ...
            background: #f5f5f5;
            color: #333;
            -webkit-transition: color 1s;
            -moz-transition: color 1s;
            transition: color 1s;
        }

#### 逻辑规范

-  尽量不使用 !important 声明

- 在特殊环境中（如：播放控件全屏），期望显示在最上层的元素，通过标签内联和 !important，将 z-index 指定为 2147483647

- 在可以使用缩写的情况下，尽量使用属性缩写，例：

        // good code
        .post {
            font: 12px/1.5 arial, sans-serif;
        }

        // bad code
        .post {
            font-family: arial, sans-serif;
            font-size: 12px;
            line-height: 1.5;
        }

- 如无必要，不得为 id、class 选择器添加类型选择器进行限定，例：

        // good code
        #error,
        .danger-message {
            font-color: #c00;
        }

        // bad code
        dialog#error,
        p.danger-message {
            font-color: #c00;
        }

- 当属性值为 0 - 1 之间的小数时，省略整数部分的 0，例：

        // good code
        .panel {
            opacity: .8;
        }

        // bad code
        .panel {
            opacity: 0.8;
        }

- url() 函数中的路径可以省略引号，url() 值中的绝对路径可省去协议名，例：

        body {
            background: url(//baidu.com/img/bg.png) no-repeat 0 0;
        }

- 颜色值不允许使用命名色值，RGB颜色值尽量使用十六进制记号形式 #rrggbb，非alpha通道的情况，不建议使用 rgb()，例：

         // good code
        .success {
            border-color: #008000;
            background-color: #aca;
            box-shadow: 0 0 2px rgba(0, 128, 0, .3);
        }

        // bad code
        .success {
            background-color: lightgreen;
        }
       

- font-family 按「西文字体在前、中文字体在后」、「效果佳 (质量高/更能满足需求) 的字体在前、效果一般的字体在后」的顺序编写，最后必须指定一个通用字体族( serif / sans-serif )，例：

        /* Display according to platform */
        .article {
            font-family: Arial, sans-serif;
        }

        /* Specific for most platforms */
        h1 {
            font-family: "Helvetica Neue", Arial, "Hiragino Sans GB", "WenQuanYi Micro Hei", "Microsoft YaHei", sans-serif;
        }

- 需要在 Windows 平台显示的中文内容，其字号应不小于 12px，由于 Windows 的字体渲染机制，小于 12px 的文字显示效果极差、难以辨认

- 任何时候都需要开启字体抗锯齿属性，代码：

        body {
          text-rendering: optimizeLegibility!important;
          -webkit-font-smoothing: antialiased!important;
          -moz-osx-font-smoothing: grayscale!important;
        }

- line-height 在定义文本段落时，应尽量使用数值，即1.x / 2.0，将 line-height 设置为数值，浏览器会基于当前元素设置的 font-size 进行再次计算。在不同字号的文本段落组合中，能达到较为舒适的行间间隔效果，避免在每个设置了 font-size 都需要设置 line-height。但当 line-height 用于控制垂直居中时，还是应该设置成与容器高度一致（即PX单位）。

- 使用高性能的动画属性，如：使用 translate 来代替 left 作为动画属性

- Media Query 如果有多个逗号分隔的条件时，应将每个条件放在单独一行中，例：

        @media
        (-webkit-min-device-pixel-ratio: 2), /* Webkit-based browsers */
        (min--moz-device-pixel-ratio: 2),    /* Older Firefox browsers (prior to Firefox 16) */
        (min-resolution: 2dppx),             /* The standard way */
        (min-resolution: 192dpi) {           /* dppx fallback */
            /* Retina-specific stuff here */
        }

 - 需要添加 hack 时应尽可能考虑是否可以采用其他方式解决，必须CssHack的话，尽量使用 选择器 hack 处理兼容性，而非 属性 hack，例：

        /* IE 7 */
        *:first-child + html #header {
            margin-top: 3px;
           padding: 5px;
        }

        /* IE 6 */
        * html #header {
            margin-top: 5px;
            padding: 4px;
        }

> [参考文献 （guide - Css编码规范）](https://github.com/surmon-china/spec/blob/master/css-style-guide.md)

***

### 编译型Css语言编译规范

> 下文中 “Less” 代指所有编译型Css动态语言

#### 项目应用

-  在使用Less + Bootstrap的项目中，应基于Bootstrap文件夹本身的基础上独立出项目的文件夹，并尽量不在框架本身做修改，同时由一个Core.less文件驱动

- Less项目中，无论是否使用框架，文件结构都应该至少由一个项目Core.less文件 + 一个项目文件夹组成

- 尽量避免一个/多个文件中覆盖变量，或重复声明变量的行为

- 对于复用性较强的模块，根据其性质，用以下两种方法处理，而避免多处Copy造成冗余和降低可维护性的情况

    * 封装为Mixins，在编译时引用
  
    * 放置在全局css中，在html中使用选择器名称引用

- 项目文件夹内的结构应按照UI结构分为：
    
    * base.less（放置全局基础属性，如*/html/body/css reset/等）

    * common.less（放置全局公用属性，如btn/form/text/等）

    * layout.less（放置footer/header/aside/nav/等主体结构）

    * variables.less（Less变量，用于代替Bootstrap默认变量文件）

    * iconfont.less（图标字体）

    * 各子页面/子模块 的独立less文件（如：user.less、login.less、player.less、article.less）

- 在项目主Core.less文件中，需创建和项目Core.less同名的.md文件，将常用变量/mixins的引用方式/整理归类并保存至此文件中，以便使用

- 使用自动化工具编译less文件时，需添加Sourcemap，供浏览器调试使用，详见自动化部分

#### 代码组织

- 代码必须（MUST）按如下形式按顺序组织：
        1.  @import
        2.  变量声明
        3.  样式声明

        // 基础结构
        @import "est/all.less";

        @default-text-color: #333;

        .page {
            width: 960px;
            margin: 0 auto;
        }
- @import 语句引用的文件必须写在一对引号内，.less 后缀不得省略（与引入 CSS 文件时的路径格式一致）。引号使用 ' 和 " 均可，但在同一项目内必须统一，例：

        // bad code
        @import 'est/all';
        @import "my/mixins.less";

        // good code
        @import "est/all.less";
        @import "my/mixins.less";

- Less 的变量值总是以同一作用域下最后一个同名变量为准，后面的设定会覆盖所有之前的设定，所以任何时候都因该避免一个/多个文件中覆盖变量，或重复声明变量的行为

- 变量命名必须采用 @foo-bar（连字符） 形式，不得使用 @fooBar （驼峰）形式，务必注意！

#### 书写规范

- 与CSS/JS的规范相同，实例：

        // 注意空格与空格位置

        // bad code
        .box{
            @w:50px;
            @h :30px;
            width:@w;
            height :@h;
            color: rgba(255,255,255,.3);
            transition: width 1s,height 3s;
        }

        // good code
        .box {
            @w: 50px;
            @h: 30px;
            width: @w;
            height: @h;
            transition: width 1s, height 3s;
        }



        // 运算中的空格符

        // bad code
        @a: 200px;
        @b: (@a+100)*2;

        // good code
        @a: 200px;
        @b: (@a + 100px) * 2;


        // Mixin（类似function） 和后面的空格之间不得包含空格，就像这样
        .box {
            .size(30px, 20px);
            .clearfix();
        }

        // 多选择器必须独占一行，就像这样
        h1,
        h2,
        h3 {
            font-weight: 700;
        }

        // 能用mixins的一定要用mixins，这也是less存在的意义之一
        // bad code
        .box {
            -webkit-transform: rotate(30deg);
               -moz-transform: rotate(30deg);
                -ms-transform: rotate(30deg);
                 -o-transform: rotate(30deg);
                    transform: rotate(30deg);
        }

        // good code
        .box {
             @include transform(rotate(30deg));
        }

- 使用继承时，如果在声明块内书写 :extend 语句，必须写在开头，例：

        // bad code
        .sub {
            color: red;
            &:extend(.mod all);
        }

        // good code
        .sub {
            &:extend(.mod all);
            color: red;
        }

- 一定要注意Mixin模块，是否是一个需要使用的模块，是否需要参数，是否本身输出内容，在使用时，则分不同的情况来决定使用时是否需要加上小括号，例：

        // 错误方法
        .big-text {
            font-size: 2em;
        }

        h3 {
            .big-text;
        }

        // 正确方法
        .big-text() {
            font-size: 2em;
        }

        h3 {
            .big-text();
        }
        

        // 如果混入的是本身不输出内容的 mixin，必须（MUST）在 mixin 后添加括号（即使不传参数），以区分这是否是一个 className（修改以后是否会影响 HTML）

        // 错误使用
        .box {
            .clearfix;
            .size (20px);
        }

        // 正确使用
        .box {
            .clearfix();
            .size(20px);
        }

        // Mixin 的参数分隔符使用 ,分割，祥参考语法规范。

> [参考文献 （guide - Less编码规范）](https://github.com/surmon-china/spec/blob/master/less-code-style.md)