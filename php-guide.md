## coding style
#### 沿用Laravel的编码方式，遵循PSR2和PSR4标准
> Laravel follows the [PSR-2](https://github.com/PizzaLiu/PHP-FIG/blob/master/PSR-2-coding-style-guide-cn.md) coding standard and the [PSR-4](https://github.com/PizzaLiu/PHP-FIG/blob/master/PSR-4-autoloader-cn.md) autoloading standard.

##### 注意，代码提交前使用[php-cs-fixer](https://github.com/FriendsOfPHP/PHP-CS-Fixer)进行检查修复 #####

#### 补充说明
- 变量命名使用小写字母和下划线的方式，例如` $user_profile`（为了与前端表单name的命名统一起来）。
- 常量以大写字母和下划线命名，例如 `HAS_ONE`和 `MANY_TO_MANY`；
-  函数命名使用小写字母和下划线的方式，例如 `get_client_ip`；
  <pre>
    public function get_client_ip()
    {
    }

</pre>

- 成员方法的命名使用小驼峰法，即首字母小写, 例如 getUserName；
  <pre>
    public function getUserName()
    {
    }

</pre>

- 类属性的命名使用小写字母方式；
  <pre>private $table_name;</pre>

- 所有变量、方法等使用具有明确含义的英文单词命名，比如getUserNameByID方法, $user_id变量

- 运算符、小括号、关键词和函数
    每个运算符与两边参与运算的值或表达式中间要有一个空格，唯一的特例是字符连接运算符号 . 两边不加空格；
    $result = (($a + 1) * 3 / 2 + $num)).'Test';
    $condition ? func1($var) : func2($var);
    每段较大的程序体，上、下应当加入空白行，两个程序块之间只使用1个空行，禁止使用多行。少于15行的程序块，可不加上下空白行。



- 引号
    PHP中单引号和双引号具有不同的含义，最大的几项区别如下：    
    1.单引号中，任何变量($var)、特殊转义字符(如 \t \r \n 等)    不会被解析，因此PHP的解析速度更快，转义字符仅仅支持 \' 和 \\ 这样对单引号和反斜杠本身的转义；    
    2.双引号中，变量($var)值会代入字符串中，特殊转义字符也会被解析成特定的单个字符，这样虽然程序编写更加方便，但同时PHP的解析也很慢；   
数组中，如果下标不是整型，而是字符串类型，请务必用单引号将下标括起，正确的写法为$array['key']，而不是$array[key]；因为不正确的写法会使PHP解析器认为key是一个常量，进而先判断常量是否存在，不存在时才以 key 作为下标带入表达式中，同时出发错误事件，产生一条Notice级错误。    
    3.因此，在绝大多数可以使用单引号的场合，禁止使用双引号。    

    依据上述分析，可以或必须使用单引号的情况包括但不限于下述：    
    1.字符串为固定值，不包含 `\t` 等特殊转义字符；    
    2.数组的固定下标，例如：`$array['key'];`；    
    3.表达式中不需要带入变量，例如：`$string = 'test';`， 而非：`$string = "test$var";`

#### 本地开发及提交流程
- 建议使用PHP代码格式化插件，比如Sublime的[phpfmt](https://github.com/phpfmt/sublime-phpfmt)开启psr2规范后可在保存时自动格式化
- 提交前使用[php-cs-fixer](https://github.com/FriendsOfPHP/PHP-CS-Fixer)进行再次修复
- 确认无误后提交至对应的分支即可
