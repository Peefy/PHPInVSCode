
# PHP In VS Code

## PHP简介

PHP（全称：PHP：Hypertext Preprocessor，即"PHP：超文本预处理器"）是一种通用开源脚本语言。

PHP 文件可包含文本、HTML、JavaScript代码和 PHP 代码

PHP 代码在服务器上执行，结果以纯 HTML 形式返回给浏览器

**PHP的作用**

* PHP 可以生成动态页面内容
* PHP 可以创建、打开、读取、写入、关闭服务器上的文件
* PHP 可以收集表单数据
* PHP 可以发送和接收 cookies
* PHP 可以添加、删除、修改您的数据库中的数据
* PHP 可以限制用户访问您的网站上的一些页面
* PHP 可以加密数据

## PHP语法

PHP 脚本可以放在文档中的任何位置。PHP 脚本以 <?php 开始，以 ?> 结束：

```php
<!DOCTYPE html>
<html>
<body>

<h1>My first PHP page</h1>

<?php
echo "Hello World!";
?>

</body>
</html>
```

**PHP 中的注释**

```php
<!DOCTYPE html>
<html>
<body>

<?php
// 这是 PHP 单行注释

/*
这是
PHP 多行
注释
*/
?>

</body>
</html>
```

## PHP 变量

与代数类似，可以给 PHP 变量赋予某个值（x=5）或者表达式（z=x+y）。

变量可以是很短的名称（如 x 和 y）或者更具描述性的名称（如 age、carname、totalvolume）。

PHP 变量规则：

* 变量以 $ 符号开始，后面跟着变量的名称
* 变量名必须以字母或者下划线字符开始
* 变量名只能包含字母数字字符以及下划线（A-z、0-9 和 _ ）
* 变量名不能包含空格
* 变量名是区分大小写的（$y 和 $Y 是两个不同的变量）

```php
<?php
$txt="Hello world!";
$x=5;
$y=10.5;
?>
```


PHP 是一门弱类型语言。PHP 变量作用域
变量的作用域是脚本中变量可被引用/使用的部分。
PHP 有四种不同的变量作用域：

* **local**
* **global**
* **static**
* **parameter**

**局部和全局作用域**-在所有函数外部定义的变量，拥有全局作用域。除了函数外，全局变量可以被脚本中的任何部分访问，要在一个函数中访问一个全局变量，需要使用 global 关键字。在 PHP 函数内部声明的变量是局部变量，仅能在函数内部访问：

```php
<?php
$x=5; // 全局变量

function myTest()
{
    $y=10; // 局部变量
    echo "<p>测试函数内变量:<p>";
    echo "变量 x 为: $x";
    echo "<br>";
    echo "变量 y 为: $y";
} 

myTest();

echo "<p>测试函数外变量:<p>";
echo "变量 x 为: $x";
echo "<br>";
echo "变量 y 为: $y";
?>
```

在以上实例中 myTest() 函数定义了 $x 和 $y 变量。 $x 变量在函数外声明，所以它是全局变量 ， $y 变量在函数内声明所以它是局部变量。

当调用myTest()函数并输出两个变量的值, 函数将会输出局部变量 $y 的值，但是不能输出 $x 的值，因为 $x 变量在函数外定义，无法在函数内使用，如果要在一个函数中访问一个全局变量，需要使用 global 关键字。

然后在myTest()函数外输出两个变量的值，函数将会输出全局变量 $x 的值，但是不能输出 $y 的值，因为 $y 变量在函数中定义，属于局部变量。

global 关键字用于函数内访问全局变量。

在函数内调用函数外定义的全局变量，我们需要在函数中的变量前加上 global 关键字：

```php
<?php
$x=5;
$y=10;
 
function myTest()
{
    global $x,$y;
    $y=$x+$y;
}
 
myTest();
echo $y; // 输出 15
?>
```

PHP 将所有全局变量存储在一个名为 $GLOBALS[index] 的数组中。 index 保存变量的名称。这个数组可以在函数内部访问，也可以直接用来更新全局变量。

```php
<?php
$x=5;
$y=10;
 
function myTest()
{
    $GLOBALS['y']=$GLOBALS['x']+$GLOBALS['y'];
} 
 
myTest();
echo $y;
?>
```

**Static 作用域**-当一个函数完成时，它的所有变量通常都会被删除。然而，有时候希望某个局部变量不要被删除。要做到这一点，请在第一次声明变量时使用 static 关键字(类似C语言函数内部变量使用static关键字)：

```php
<?php
function myTest()
{
    static $x=0;
    echo $x;
    $x++;
    echo PHP_EOL;    // 换行符
}
 
myTest();
myTest();
myTest();
?>
```

## PHP echo 和 print 语句

在 PHP 中有两个基本的输出方式： echo 和 print。

echo 和 print 区别:

* echo - 可以输出一个或多个字符串
* print - 只允许输出一个字符串，返回值总为 1

echo 是一个语言结构，使用的时候可以不用加括号，也可以加上括号： echo 或 echo()。

```php
<?php
echo "<h2>PHP 很有趣!</h2>";
echo "Hello world!<br>";
echo "我要学 PHP!<br>";
echo "这是一个", "字符串，", "使用了", "多个", "参数。";
?>
```

```php
<?php
$txt1="学习 PHP";
$txt2="RUNOOB.COM";
$cars=array("Volvo","BMW","Toyota");
 
echo $txt1;
echo "<br>";
echo "在 $txt2 学习 PHP ";
echo "<br>";
echo "我车的品牌是 {$cars[0]}";
?>
```

print 同样是一个语言结构，可以使用括号，也可以不使用括号： print 或 print()。

## PHP EOF(heredoc) 使用说明

PHP EOF(heredoc)是一种在命令行shell（如sh、csh、ksh、bash、PowerShell和zsh）和程序语言（像Perl、PHP、Python和Ruby）里定义一个字符串的方法。

使用概述：

1. 必须后接分号，否则编译通不过。
2. EOF 可以用任意其它字符代替，只需保证结束标识与开始标识一致。
3. 结束标识必须顶格独自占一行(即必须从行首开始，前后不能衔接任何空白和字符)。
4. 开始标识可以不带引号或带单双引号，不带引号与带双引号效果一致，解释内嵌的变量和转义符号，带单引号则不解释内嵌的变量和转义符号。
5. 当内容需要内嵌引号（单引号或双引号）时，不需要加转义符，本身对单双引号转义，此处相当与q和qq的用法。

```php
<?php
echo <<<EOF
        <h1>我的第一个标题</h1>
        <p>我的第一个段落。</p>
EOF;
// 结束需要独立一行且前后不能空格
?>
```

注意：

1.以 `<<<EOF` 开始标记开始，以 EOF 结束标记结束，结束标记必须顶头写，不能有缩进和空格，且在结束标记末尾要有分号 。

2.开始标记和结束标记相同，比如常用大写的 EOT、EOD、EOF 来表示，但是不只限于那几个(也可以用：JSON、HTML等)，只要保证开始标记和结束标记不在正文中出现即可。

3.位于开始标记和结束标记之间的变量可以被正常解析，但是函数则不可以。在 heredoc 中，变量不需要用连接符 . 或 , 来拼接，如下：

```php
<?php
$name="runoob";
$a= <<<EOF
        "abc"$name
        "123"
EOF;
// 结束需要独立一行且前后不能空格
echo $a;
?>
```

## PHP 数据类型

String（字符串）, Integer（整型）, Float（浮点型）, Boolean（布尔型）, Array（数组）, Object（对象）, NULL（空值）。

**PHP 字符串**-一个字符串是一串字符的序列，就像 "Hello world!"。可以将任何文本放在单引号和双引号中：

```php
<?php 
$x = "Hello world!";
echo $x;
echo "<br>"; 
$x = 'Hello world!';
echo $x;
?>
```

**PHP 整型**-整数是一个没有小数的数字。整数规则:

* 整数必须至少有一个数字 (0-9)
* 整数不能包含逗号或空格
* 整数是没有小数点的
* 整数可以是正数或负数
* 整型可以用三种格式来指定：十进制， 十六进制（ 以 0x 为前缀）或八进制（前缀为 0）。

```php
<?php 
$x = 5985;
var_dump($x);
echo "<br>"; 
$x = -345; // 负数 
var_dump($x);
echo "<br>"; 
$x = 0x8C; // 十六进制数
var_dump($x);
echo "<br>";
$x = 047; // 八进制数
var_dump($x);
?>
```

**PHP 浮点型**-浮点数是带小数部分的数字，或是指数形式。在以下实例中我们将测试不同的数字。 

```php
<?php 
$x = 10.365;
var_dump($x);
echo "<br>"; 
$x = 2.4e3;
var_dump($x);
echo "<br>"; 
$x = 8E-5;
var_dump($x);
?>
```

**PHP 布尔型。**布尔型可以是 TRUE 或 FALSE。

```php
$x=true;
$y=false;
```

**PHP 数组**-数组可以在一个变量中存储多个值。

在以下实例中创建了一个数组， 然后使用 PHP var_dump() 函数返回数组的数据类型和值：

```php
<?php 
$cars=array("Volvo","BMW","Toyota");
var_dump($cars);
?>
```

**PHP 对象**-对象数据类型也可以用于存储数据。在 PHP 中，对象必须声明。首先，必须使用class关键字声明类对象。类是可以包含属性和方法的结构。然后我们在类中定义数据类型，然后在实例化的类中使用数据类型：

```php
<?php
class Car
{
  var $color;
  function __construct($color="green") {
    $this->color = $color;
  }
  function what_color() {
    return $this->color;
  }
}
?>
```

**PHP NULL 值**-NULL 值表示变量没有值。NULL 是数据类型为 NULL 的值。

NULL 值指明一个变量是否为空值。 同样可用于数据空值和NULL值的区别。

可以通过设置变量值为 NULL 来清空变量数据：

```php
<?php
$x="Hello world!";
$x=null;
var_dump($x);
?>
```

## PHP 类型比较
