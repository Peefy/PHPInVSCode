
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
* PHP 可以添加、删除、修改的数据库中的数据
* PHP 可以限制用户访问的网站上的一些页面
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

在函数内调用函数外定义的全局变量，需要在函数中的变量前加上 global 关键字：

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
$txt2="";
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

**PHP 浮点型**-浮点数是带小数部分的数字，或是指数形式。在以下实例中将测试不同的数字。 

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

**PHP 对象**-对象数据类型也可以用于存储数据。在 PHP 中，对象必须声明。首先，必须使用class关键字声明类对象。类是可以包含属性和方法的结构。然后在类中定义数据类型，然后在实例化的类中使用数据类型：

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

虽然 PHP 是弱类型语言，但也需要明白变量类型及它们的意义，因为经常需要对 PHP 变量进行比较，包含松散和严格比较。

* **松散比较**：使用两个等号 == 比较，只比较值，不比较类型。
* **严格比较**：用三个等号 === 比较，除了比较值，也比较类型。

```php
<?php
if(42 == "42") {
    echo '1、值相等';
}
 
echo PHP_EOL; // 换行符
 
if(42 === "42") {
    echo '2、类型相等';
} else {
    echo '3、不相等';
}
?>
```

**PHP中 比较 0、false、null**

```php
<?php
echo '0 == false: ';
var_dump(0 == false);
echo '0 === false: ';
var_dump(0 === false);
echo PHP_EOL;
echo '0 == null: ';
var_dump(0 == null);
echo '0 === null: ';
var_dump(0 === null);
echo PHP_EOL;
echo 'false == null: ';
var_dump(false == null);
echo 'false === null: ';
var_dump(false === null);
echo PHP_EOL;
echo '"0" == false: ';
var_dump("0" == false);
echo '"0" === false: ';
var_dump("0" === false);
echo PHP_EOL;
echo '"0" == null: ';
var_dump("0" == null);
echo '"0" === null: ';
var_dump("0" === null);
echo PHP_EOL;
echo '"" == false: ';
var_dump("" == false);
echo '"" === false: ';
var_dump("" === false);
echo PHP_EOL;
echo '"" == null: ';
var_dump("" == null);
echo '"" === null: ';
var_dump("" === null);
```

以上实例输出结果为:

```php
0 == false: bool(true)
0 === false: bool(false)

0 == null: bool(true)
0 === null: bool(false)

false == null: bool(true)
false === null: bool(false)

"0" == false: bool(true)
"0" === false: bool(false)

"0" == null: bool(false)
"0" === null: bool(false)

"" == false: bool(true)
"" === false: bool(false)

"" == null: bool(true)
"" === null: bool(false)
```

## PHP 常量

常量值被定义后，在脚本的其他任何地方都不能被改变。常量是一个简单值的标识符。该值在脚本中不能改变。

一个常量由英文字母、下划线、和数字组成,但数字不能作为首字母出现。 (常量名不需要加 $ 修饰符)。

注意： 常量在整个脚本中都可以使用。

设置常量，使用 define() 函数，函数语法如下：

```php
bool define ( string $name , mixed $value [, bool $case_insensitive = false ] )
```

该函数有三个参数:

* **name**：必选参数，常量名称，即标志符。
* **value**：必选参数，常量的值。
* **case_insensitive** ：可选参数，如果设置为 TRUE，该常量则大小写不敏感。默认是大小写敏感的。

```php
<?php
// 区分大小写的常量名
define("GREETING", "欢迎访问 ");
echo GREETING;    // 输出 "欢迎访问 "
echo '<br>';
echo greeting;   // 输出 "greeting"
?>
```

常量在定义后，默认是全局变量，可以在整个运行的脚本的任何地方使用。

以下实例演示了在函数内使用常量，即便常量定义在函数外也可以正常使用常量。

```php
<?php
define("GREETING", "欢迎访问 ");
 
function myTest() {
    echo GREETING;
}
 
myTest();    // 输出 "欢迎访问 "
?>
```

## PHP 字符串变量

字符串变量用于包含有字符的值。

在创建字符串之后，就可以对它进行操作了。可以直接在函数中使用字符串，或者把它存储在变量中。

```php
<?php
$txt="Hello world!";
echo $txt;
?>
```

在 PHP 中，只有一个字符串运算符。并置运算符 (`.`) 用于把两个字符串值连接起来。

strlen() 函数返回字符串的长度（字节数）。

strpos() 函数用于在字符串内查找一个字符或一段指定的文本。如果在字符串中找到匹配，该函数会返回第一个匹配的字符位置。如果未找到匹配，则返回 FALSE。

```php
<?php
$txt1="Hello world!";
$txt2="What a nice day!";
echo $txt1 . " " . $txt2;
echo strlen("Hello world!");
echo strpos("Hello world!","world");
?>
```

## PHP 运算符

**算术运算符**

加`+`,减`-`,乘`*`,除`/`,取余`%`,取负`-`,并置`.`

```php
<?php 
$x=10; 
$y=6;
echo ($x + $y); // 输出16
echo '<br>';  // 换行
 
echo ($x - $y); // 输出4
echo '<br>';  // 换行
 
echo ($x * $y); // 输出60
echo '<br>';  // 换行
 
echo ($x / $y); // 输出1.6666666666667
echo '<br>';  // 换行
 
echo ($x % $y); // 输出4
echo '<br>';  // 换行
 
echo -$x;
?>
```

PHP7+ 版本新增整除运算符 intdiv(),使用实例：

```php
<?php
var_dump(intdiv(10, 3));
?>
```

**赋值运算符**

`x = y`	,`x += y`	,`x -= y`	,`x *= y`	,`x /= y`	,`x %= y`	,`a .= b`

```php
<?php 
$x=10; 
echo $x; // 输出10
 
$y=20; 
$y += 100;
echo $y; // 输出120
 
$z=50;
$z -= 25;
echo $z; // 输出25
 
$i=5;
$i *= 6;
echo $i; // 输出30
 
$j=10;
$j /= 5;
echo $j; // 输出2
 
$k=15;
$k %= 4;
echo $k; // 输出3
?>
```

**递增/递减运算符**

`x++`,`++x`,`--x`,`x--`

```php
<?php
$x=10; 
echo ++$x; // 输出11
 
$y=10; 
echo $y++; // 输出10
 
$z=5;
echo --$z; // 输出4
 
$i=5;
echo $i--; // 输出5
?>
```

**比较运算符**

`x == y`,`x === y`	,`x != y`	,`x <> y`	,`x !== y`	,`x > y`	,`x < y`	,`x >= y`	,`x <= y`

```php
<?php
$x=100; 
$y="100";
 
var_dump($x == $y);
echo "<br>";
var_dump($x === $y);
echo "<br>";
var_dump($x != $y);
echo "<br>";
var_dump($x !== $y);
echo "<br>";
 
$a=50;
$b=90;
 
var_dump($a > $b);
echo "<br>";
var_dump($a < $b);
?>
```

**逻辑运算符**

`x and y`	
`x or y`	
`x xor y`	
`x && y`
`x || y`	
`! x`

**数组运算符**

x + y	集合	x 和 y 的集合

x == y	相等	如果 x 和 y 具有相同的键/值对，则返回 true

x === y	恒等	如果 x 和 y 具有相同的键/值对，且顺序相同类型相同，则返回 true

x != y	不相等	如果 x 不等于 y，则返回 true

x <> y	不相等	如果 x 不等于 y，则返回 true

x !== y

```php
<?php
$x = array("a" => "red", "b" => "green"); 
$y = array("c" => "blue", "d" => "yellow"); 
$z = $x + $y; // $x 和 $y 数组合并
var_dump($z);
var_dump($x == $y);
var_dump($x === $y);
var_dump($x != $y);
var_dump($x <> $y);
var_dump($x !== $y);
?>
```

**三元运算符**

```
(expr1) ? (expr2) : (expr3) 
```

**NULL 合并运算符 ??**

```php
<?php
// 如果 $_GET['user'] 不存在返回 'nobody'，否则返回 $_GET['user'] 的值
$username = $_GET['user'] ?? 'nobody';
// 类似的三元运算符
$username = isset($_GET['user']) ? $_GET['user'] : 'nobody';
?>
```

**组合比较符 <=>**

`$c = $a <=> $b;`解析如下：

* 如果 $a > $b, 则 $c 的值为 1。
* 如果 $a == $b, 则 $c 的值为 0。
* 如果 $a < $b, 则 $c 的值为 -1。

```php
<?php
// 整型
echo 1 <=> 1; // 0
echo 1 <=> 2; // -1
echo 2 <=> 1; // 1
 
// 浮点型
echo 1.5 <=> 1.5; // 0
echo 1.5 <=> 2.5; // -1
echo 2.5 <=> 1.5; // 1
 
// 字符串
echo "a" <=> "a"; // 0
echo "a" <=> "b"; // -1
echo "b" <=> "a"; // 1
?>
```

**位运算符**

`<<`,`>>`

**类型运算符**

`instanceof`

## PHP 条件语句

在 PHP 中，提供了下列条件语句：

* if 语句 - 在条件成立时执行代码
* if...else 语句 - 在条件成立时执行一块代码，条件不成立时执行另一块代码
* if...elseif....else 语句 - 在若干条件之一成立时执行一个代码块
* switch 语句 - 在若干条件之一成立时执行一个代码块

```php
<?php
$t=date("H");
if ($t<"20")
{
    echo "Have a good day!";
}
?>
```

```php
<?php
$t=date("H");
if ($t<"20")
{
    echo "Have a good day!";
}
else
{
    echo "Have a good night!";
}
?>
```

```php
<?php
$t=date("H");
if ($t<"10")
{
    echo "Have a good morning!";
}
elseif ($t<"20")
{
    echo "Have a good day!";
}
else
{
    echo "Have a good night!";
}
?>
```

## PHP Switch 语句

```php
<?php
$favcolor="red";
switch ($favcolor)
{
case "red":
    echo "你喜欢的颜色是红色!";
    break;
case "blue":
    echo "你喜欢的颜色是蓝色!";
    break;
case "green":
    echo "你喜欢的颜色是绿色!";
    break;
default:
    echo "你喜欢的颜色不是 红, 蓝, 或绿色!";
}
?>
```

## PHP 数组

在 PHP 中，有三种类型的数组：

* **数值数组** - 带有数字 ID 键的数组
* **关联数组** - 带有指定的键的数组，每个键关联一个值
* **多维数组** - 包含一个或多个数组的数组

```php
<?php
$cars=array("Volvo","BMW","Toyota");
echo "I like " . $cars[0] . ", " . $cars[1] . " and " . $cars[2] . ".";
$arrlength=count($cars);
 for($x=0;$x<$arrlength;$x++)
{
    echo $cars[$x];
    echo "<br>";
}
?>
```
count() 函数用于返回数组的长度（元素的数量）：

关联数组

```php
<?php
$age=array("Peter"=>"35","Ben"=>"37","Joe"=>"43");
echo "Peter is " . $age['Peter'] . " years old.";
foreach($age as $x=>$x_value)
{
    echo "Key=" . $x . ", Value=" . $x_value;
    echo "<br>";
}
?>
```

数组中的元素可以按字母或数字顺序进行降序或升序排列。

* sort() - 对数组进行升序排列
* rsort() - 对数组进行降序排列
* asort() - 根据关联数组的值，对数组进行升序排列
* ksort() - 根据关联数组的键，对数组进行升序排列
* arsort() - 根据关联数组的值，对数组进行降序排列
* krsort() - 根据关联数组的键，对数组进行降序排列

## PHP 超级全局变量

超级全局变量在PHP 4.1.0之后被启用, 是PHP系统中自带的变量，在一个脚本的全部作用域中都可用。

PHP 超级全局变量列表:

* $GLOBALS 一个包含了全部变量的全局组合数组。变量的名字就是数组的键。
* $_SERVER 一个包含了诸如头信息(header)、路径(path)、以及脚本位置(script locations)等等信息的数组。
* $_REQUEST 用于收集HTML表单提交的数据。
* $_POST  被广泛应用于收集表单数据，在HTML form标签的指定该属性："method="post"。
* $_GET  $_GET 同样被广泛应用于收集表单数据，在HTML form标签的指定该属性："method="get"。
* $_FILES
* $_ENV
* $_COOKIE
* $_SESSION

## PHP 循环

* while - 只要指定的条件成立，则循环执行代码块
* do...while - 首先执行一次代码块，然后在指定的条件成立时重复这个循环
* for - 循环执行代码块指定的次数
* foreach - 根据数组中每个元素来循环代码块

```php
<html>
<body>

<?php
$i=1;
while($i<=5)
{
    echo "The number is " . $i . "<br>";
    $i++;
}

$i=1;
do
{
    $i++;
    echo "The number is " . $i . "<br>";
}
while ($i<=5);

for ($i=1; $i<=5; $i++)
{
    echo "The number is " . $i . "<br>";
}

$x=array("one","two","three");
foreach ($x as $value)
{
    echo $value . "<br>";
}
?>

</body>
</html>
```

## PHP 函数

在 PHP 中，提供了超过 1000 个内建的函数。

```php
<?php
function writeNameWith($fname)
{
    echo $fname . " Refsnes.<br>";
    return $fname
}

function writeName()
{
    echo "Kai Jim Refsnes";
}
 
echo "My name is ";
writeName();
?>
```

## PHP 魔术常量

* `__LINE__`-文件中的当前行号。
* `__FILE__`-文件的完整路径和文件名
* `__DIR__`-文件所在的目录
* `__FUNCTION__`-函数名称
* `__CLASS__`-类的名称
* `__TRAIT__`-Trait 名包括其被声明的作用区域（例如 Foo\Bar）。
* `__METHOD__`-类的方法名（PHP 5.0.0 新加）。返回该方法被定义时的名字（区分大小写）。
* `__NAMESPACE`-当前命名空间的名称（区分大小写）

## PHP 命名空间(namespace)

```php
<?php  
namespace MyProject;

const CONNECT_OK = 1;
class Connection { /* ... */ }
function connect() { /* ... */  }

namespace AnotherProject;

const CONNECT_OK = 1;
class Connection { /* ... */ }
function connect() { /* ... */  }
?>  
```

```php
<?php
namespace MyProject {
    const CONNECT_OK = 1;
    class Connection { /* ... */ }
    function connect() { /* ... */  }
}

namespace AnotherProject {
    const CONNECT_OK = 1;
    class Connection { /* ... */ }
    function connect() { /* ... */  }
}

namespace { // 全局代码
session_start();
$a = MyProject\connect();
echo MyProject\Connection::start();
}
?>
```

PHP 命名空间中的类名可以通过三种方式引用：

* 非限定名称，或不包含前缀的类名称，例如 $a=new foo(); 或 foo::staticmethod();。如果当前命名空间是 currentnamespace，foo 将被解析为 currentnamespace\foo。如果使用 foo 的代码是全局的，不包含在任何命名空间中的代码，则 foo 会被解析为foo。 警告：如果命名空间中的函数或常量未定义，则该非限定的函数名称或常量名称会被解析为全局函数名称或常量名称。

* 限定名称,或包含前缀的名称，例如 $a = new subnamespace\foo(); 或 subnamespace\foo::staticmethod();。如果当前的命名空间是 currentnamespace，则 foo 会被解析为 currentnamespace\subnamespace\foo。如果使用 foo 的代码是全局的，不包含在任何命名空间中的代码，foo 会被解析为subnamespace\foo。

* 完全限定名称，或包含了全局前缀操作符的名称，例如， $a = new \currentnamespace\foo(); 或 \currentnamespace\foo::staticmethod();。在这种情况下，foo 总是被解析为代码中的文字名(literal name)currentnamespace\foo。

关键字 namespace 可用来显式访问当前命名空间或子命名空间中的元素。它等价于类中的 self 操作符。

namespace操作符，命名空间中的代码


```php
<?php
namespace MyProject;

use blah\blah as mine; // see "Using namespaces: importing/aliasing"

blah\mine(); // calls function blah\blah\mine()
namespace\blah\mine(); // calls function MyProject\blah\mine()

namespace\func(); // calls function MyProject\func()
namespace\sub\func(); // calls function MyProject\sub\func()
namespace\cname::method(); // calls static method "method" of class MyProject\cname
$a = new namespace\sub\cname(); // instantiates object of class MyProject\sub\cname
$b = namespace\CONSTANT; // assigns value of constant MyProject\CONSTANT to $b
?>
```

使用命名空间：别名/导入

```php
<?php
namespace foo;
use My\Full\Classname as Another;

// 下面的例子与 use My\Full\NSname as NSname 相同
use My\Full\NSname;

// 导入一个全局类
use \ArrayObject;

$obj = new namespace\Another; // 实例化 foo\Another 对象
$obj = new Another; // 实例化 My\Full\Classname　对象
NSname\subns\func(); // 调用函数 My\Full\NSname\subns\func
$a = new ArrayObject(array(1)); // 实例化 ArrayObject 对象
// 如果不使用 "use \ArrayObject" ，则实例化一个 foo\ArrayObject 对象
?>
```

## PHP 面向对象

在面向对象的程序设计（英语：Object-oriented programming，缩写：OOP）中，对象是一个由信息及对信息进行处理的描述所组成的整体，是对现实世界的抽象。

对象的主要三个特性：

* 对象的行为：可以对 对象施加那些操作，开灯，关灯就是行为。
* 对象的形态：当施加那些方法是对象如何响应，颜色，尺寸，外型。
* 对象的表示：对象的表示就相当于身份证，具体区分在相同的行为与状态下有什么不同。

**面向对象内容**

* 类 − 定义了一件事物的抽象特点。类的定义包含了数据的形式以及对数据的操作。
* 对象 − 是类的实例。
* 成员变量 − 定义在类内部的变量。该变量的值对外是不可见的，但是可以通过成员函数访问，在类被实例化为对象后，该变量即可称为对象的属性。
* 成员函数 − 定义在类的内部，可用于访问对象的数据。
* 继承 − 继承性是子类自动共享父类数据结构和方法的机制，这是类之间的一种关系。在定义和实现一个类的时候，可以在一个已经存在的类的基础之上来进行，把这个已经存在的类所定义的内容作为自己的内容，并加入若干新的内容。
* 父类 − 一个类被其他类继承，可将该类称为父类，或基类，或超类。
* 子类 − 一个类继承其他类称为子类，也可称为派生类。
* 多态 − 多态性是指相同的函数或方法可作用于多种类型的对象上并获得不同的结果。不同的对象，收到同一消息可以产生不同的结果，这种现象称为多态性。
* 重载 − 简单说，就是函数或者方法有同样的名称，但是参数列表不相同的情形，这样的同名不同参数的函数或者方法之间，互相称之为重载函数或者方法。
* 抽象性 − 抽象性是指将具有一致的数据结构（属性）和行为（操作）的对象抽象成类。一个类就是这样一种抽象，它反映了与应用有关的重要性质，而忽略其他一些无关内容。任何类的划分都是主观的，但必须与具体的应用有关。
* 封装 − 封装是指将现实世界中存在的某个客体的属性与行为绑定在一起，并放置在一个逻辑单元内。
* 构造函数 − 主要用来在创建对象时初始化对象， 即为对象成员变量赋初始值，总与new运算符一起使用在创建对象的语句中。
* 析构函数 − 析构函数(destructor) 与构造函数相反，当对象结束其生命周期时（例如对象所在的函数已调用完毕），系统自动执行析构函数。

**php类的用法**

* 类使用 class 关键字后加上类名定义。
* 类名后的一对大括号({})内可以定义变量和方法。
* 类的变量使用 var 来声明, 变量也可以初始化值。
* 函数定义类似 PHP 函数的定义，但函数只能通过该类及其实例化的对象访问。

```php
<?php
class Site {
  /* 成员变量 */
  var $url;
  var $title;
  
  /* 成员函数 */
  function setUrl($par){
     $this->url = $par;
  }
  
  function getUrl(){
     echo $this->url . PHP_EOL;
  }
  
  function setTitle($par){
     $this->title = $par;
  }
  
  function getTitle(){
     echo $this->title . PHP_EOL;
  }
}
?>
```

类创建后，可以使用 `new` 运算符来实例化该类的对象,可以使用该对象和`->`调用成员方法，该对象的成员方法只能操作该对象的成员变量：

```php
<?php
class Site {
  /* 成员变量 */
  var $url;
  var $title;
  
  /* 成员函数 */
  function setUrl($par){
     $this->url = $par;
  }
  
  function getUrl(){
     echo $this->url . PHP_EOL;
  }
  
  function setTitle($par){
     $this->title = $par;
  }
  
  function getTitle(){
     echo $this->title . PHP_EOL;
  }
}

$taobao = new Site;
$google = new Site;

$taobao->setTitle( "淘宝" );
$google->setTitle( "Google" );

$taobao->getTitle();
$google->getTitle();

$taobao->getUrl();
$google->getUrl();
?>
```

**php构造函数**

```php
function __construct( $par1, $par2 ) {
   $this->url = $par1;
   $this->title = $par2;
}
```

**析构函数**

```php
void __destruct ( void )
```

PHP 使用关键字 extends 来继承一个类，PHP 不支持多继承.

如果从父类继承的方法不能满足子类的需求，可以对其进行改写，这个过程叫方法的覆盖（override），也称为方法的重写。

PHP 对属性或方法的访问控制，是通过在前面添加关键字 public（公有），protected（受保护）或 private（私有）来实现的。

* public（公有）：公有的类成员可以在任何地方被访问。
* protected（受保护）：受保护的类成员则可以被其自身以及其子类和父类访问。
* private（私有）：私有的类成员则只能被其定义所在的类访问。

```php
<?php
/**
 * Define MyClass
 */
class MyClass
{
    public $public = 'Public';
    protected $protected = 'Protected';
    private $private = 'Private';

    function printHello()
    {
        echo $this->public;
        echo $this->protected;
        echo $this->private;
    }
}

$obj = new MyClass();
echo $obj->public; // 这行能被正常执行
echo $obj->protected; // 这行会产生一个致命错误
echo $obj->private; // 这行也会产生一个致命错误
$obj->printHello(); // 输出 Public、Protected 和 Private


/**
 * Define MyClass2
 */
class MyClass2 extends MyClass
{
    // 可以对 public 和 protected 进行重定义，但 private 而不能
    protected $protected = 'Protected2';

    function printHello()
    {
        echo $this->public;
        echo $this->protected;
        echo $this->private;
    }
}

$obj2 = new MyClass2();
echo $obj2->public; // 这行能被正常执行
echo $obj2->private; // 未定义 private
echo $obj2->protected; // 这行会产生一个致命错误
$obj2->printHello(); // 输出 Public、Protected2 和 Undefined

?>
```

使用接口（interface），可以指定某个类必须实现哪些方法，但不需要定义这些方法的具体内容。

接口是通过 interface 关键字来定义的，就像定义一个标准的类一样，但其中定义所有的方法都是空的。

接口中定义的所有方法都必须是公有，这是接口的特性。

要实现一个接口，使用 implements 操作符。类中必须实现接口中定义的所有方法，否则会报一个致命错误。类可以实现多个接口，用逗号来分隔多个接口的名称。

```php
<?php

// 声明一个'iTemplate'接口
interface iTemplate
{
    public function setVariable($name, $var);
    public function getHtml($template);
}


// 实现接口
class Template implements iTemplate
{
    private $vars = array();
  
    public function setVariable($name, $var)
    {
        $this->vars[$name] = $var;
    }
  
    public function getHtml($template)
    {
        foreach($this->vars as $name => $value) {
            $template = str_replace('{' . $name . '}', $value, $template);
        }
 
        return $template;
    }
}
```

可以把在类中始终保持不变的值定义为常量。在定义和使用常量的时候不需要使用 $ 符号。

任何一个类，如果它里面至少有一个方法是被声明为抽象的，那么这个类就必须被声明为抽象的。

定义为抽象的类不能被实例化。

被定义为抽象的方法只是声明了其调用方式（参数），不能定义其具体的功能实现。

继承一个抽象类的时候，子类必须定义父类中的所有抽象方法；另外，这些方法的访问控制必须和父类中一样（或者更为宽松）。例如某个抽象方法被声明为受保护的，那么子类中实现的方法就应该声明为受保护的或者公有的，而不能定义为私有的。

```php
<?php
abstract class AbstractClass
{
 // 强制要求子类定义这些方法
    abstract protected function getValue();
    abstract protected function prefixValue($prefix);

    // 普通方法（非抽象方法）
    public function printOut() {
        print $this->getValue() . PHP_EOL;
    }
}

class ConcreteClass1 extends AbstractClass
{
    protected function getValue() {
        return "ConcreteClass1";
    }

    public function prefixValue($prefix) {
        return "{$prefix}ConcreteClass1";
    }
}

class ConcreteClass2 extends AbstractClass
{
    public function getValue() {
        return "ConcreteClass2";
    }

    public function prefixValue($prefix) {
        return "{$prefix}ConcreteClass2";
    }
}

$class1 = new ConcreteClass1;
$class1->printOut();
echo $class1->prefixValue('FOO_') . PHP_EOL;

$class2 = new ConcreteClass2;
$class2->printOut();
echo $class2->prefixValue('FOO_') . PHP_EOL;
?>
```

声明类属性或方法为 static(静态)，就可以不实例化类而直接访问。

静态属性不能通过一个类已实例化的对象来访问（但静态方法可以）。

由于静态方法不需要通过对象即可调用，所以伪变量 $this 在静态方法中不可用。

静态属性不可以由对象通过 -> 操作符来访问。

```php
<?php
class Foo {
  public static $my_static = 'foo';
  
  public function staticValue() {
     return self::$my_static;
  }
}

print Foo::$my_static . PHP_EOL;
$foo = new Foo();

print $foo->staticValue() . PHP_EOL;
?>    
```

PHP 5 新增了一个 final 关键字。如果父类中的方法被声明为 final，则子类无法覆盖该方法。如果一个类被声明为 final，则不能被继承。

```php
<?php
class BaseClass {
   public function test() {
       echo "BaseClass::test() called" . PHP_EOL;
   }
   
   final public function moreTesting() {
       echo "BaseClass::moreTesting() called"  . PHP_EOL;
   }
}

class ChildClass extends BaseClass {
   public function moreTesting() {
       echo "ChildClass::moreTesting() called"  . PHP_EOL;
   }
}
// 报错信息 Fatal error: Cannot override final method BaseClass::moreTesting()
?>
```

PHP 不会在子类的构造方法中自动的调用父类的构造方法。要执行父类的构造方法，需要在子类的构造方法中调用 parent::__construct() 。

```php
<?php
class BaseClass {
   function __construct() {
       print "BaseClass 类中构造方法" . PHP_EOL;
   }
}
class SubClass extends BaseClass {
   function __construct() {
       parent::__construct();  // 子类构造方法不能自动调用父类的构造方法
       print "SubClass 类中构造方法" . PHP_EOL;
   }
}
class OtherSubClass extends BaseClass {
    // 继承 BaseClass 的构造方法
}

// 调用 BaseClass 构造方法
$obj = new BaseClass();

// 调用 BaseClass、SubClass 构造方法
$obj = new SubClass();

// 调用 BaseClass 构造方法
$obj = new OtherSubClass();
?>
```

## PHP日期

PHP `date()` 函数用于格式化时间/日期。date() 函数可把时间戳格式化为可读性更好的日期和时间。时间戳是一个字符序列，表示一定的事件发生的日期/时间。

语法如下：

```php
string date ( string $format [, int $timestamp ] )
```

* format	必需。规定时间戳的格式。
* timestamp	可选。规定时间戳。默认是当前的日期和时间。

**PHP Date() - 格式化日期**-date() 函数的第一个必需参数 format 规定了如何格式化日期/时间。

* d - 代表月中的天 (01 - 31)
* m - 代表月 (01 - 12)
* Y - 代表年 (四位数)

```php
<?php
echo date("Y/m/d") . "<br>";
echo date("Y.m.d") . "<br>";
echo date("Y-m-d");
?>
```

format 字符	|说明|	返回值例子
-|-|-
日|	---|	---
d|	月份中的第几天，有前导零的 2 位数字	|01 到 31
D|	星期中的第几天，文本表示，3 个字母|	Mon 到 Sun
j|	月份中的第几天，没有前导零	|1 到 31
l（"L"的小写字母）|	星期几，完整的文本格式|Sunday 到 Saturday
N|	ISO-8601 格式数字表示的星期中的第几天（PHP 5.1.0 新加）|	1（表示星期一）到 7（表示星期天）
S|	每月天数后面的英文后缀，2 个字符|	st，nd，rd 或者 th。可以和 j 一起用
w|	星期中的第几天，数字表示|0（表示星期天）到 6（表示星期六）
z|	年份中的第几天	|0 到 365
星期|	---|	---
W|	ISO-8601 格式年份中的第几周，每周从星期一开始（PHP 4.1.0 新加的）	|例如：42（当年的第 42 周）
月|	---|	---
F|	月份，完整的文本格式|例如 January 或者 March	January 到 December
m|	数字表示的月份，有前导零	|01 到 12
M|	三个字母缩写表示的月份|	Jan 到 Dec
n|	数字表示的月份，没有前导零|	1 到 12
t|	给定月份所应有的天数	|28 到 31
年|	---	---
L	|是否为闰年	|如果是闰年为 1，否则为 0
o	|ISO-8601 格式年份数字。这和 Y 的值相同，只除了如果 ISO 的星期数（W）属于前一年或下一年，则用那一年。（PHP 5.1.0 新加）|	Examples: 1999 or 2003
Y|	4 位数字完整表示的年份	|例如：1999 或 2003
y|	2 位数字表示的年份	|例如：99 或 03
时间|	---	|---
a|	小写的上午和下午值	|am 或 pm
A|	大写的上午和下午值	|AM 或 PM
B|	Swatch Internet 标准时	|000 到 999
g|	小时，12 小时格式，没有前导零	|1 到 12
G|	小时，24 小时格式，没有前导零	|0 到 23
h|	小时，12 小时格式，有前导零	|01 到 12
H|	小时，24 小时格式，有前导零	|00 到 23
i|	有前导零的分钟数	|00 到 59>
s|	秒数，有前导零|	00 到 59>
u|	毫秒 （PHP 5.2.2 新加）。需要注意的是 date() 函数总是返回 000000 因为它只接受 integer 参数， 而 DateTime::format() 才支持毫秒。	|示例: 654321
时区|	---|	---
e|	时区标识（PHP 5.1.0 新加）	|例如：UTC，GMT，Atlantic/Azores
I|	是否为夏令时	|如果是夏令时为 1，否则为 0
O|	与格林威治时间相差的小时数	|例如：+0200
P|	与格林威治时间（GMT）的差别，小时和分钟之间有冒号分隔（PHP 5.1.3 新加）	|例如：+02:00
T|	本机所在的时区|	例如：EST，MDT（【译者注】在 Windows 下为完整文本格式，例如"Eastern Standard Time"，中文版会显示"中国标准时间"）。
Z|	时差偏移量的秒数。UTC 西边的时区偏移量总是负的，UTC 东边的时区偏移量总是正的。	|-43200 到 43200
完整的日期／时间|	---|	---
c|	ISO 8601 格式的日期（PHP 5 新加）|	2004-02-12T15:19:21+00:00
r|	RFC 822 格式的日期|	例如：Thu, 21 Dec 2000 16:01:07 +0200
U|	从 Unix 纪元（January 1 1970 00:00:00 GMT）开始至今的秒数	|参见 time()

## PHP 包含文件

在 PHP 中，可以在服务器执行 PHP 文件之前在该文件中插入一个文件的内容。

include 和 require 语句用于在执行流中插入写在其他文件中的有用的代码。

include 和 require 除了处理错误的方式不同之外，在其他方面都是相同的：

* require 生成一个致命错误（E_COMPILE_ERROR），在错误发生后脚本会停止执行。
* include 生成一个警告（E_WARNING），在错误发生后脚本会继续执行。
  
因此，如果希望继续执行，并向用户输出结果，即使包含文件已丢失，那么请使用 include。否则，在框架、CMS 或者复杂的 PHP 应用程序编程中，请始终使用 require 向执行流引用关键文件。这有助于提高应用程序的安全性和完整性，在某个关键文件意外丢失的情况下。

包含文件省去了大量的工作。这意味着可以为所有网页创建标准页头、页脚或者菜单文件。然后，在页头需要更新时，只需更新这个页头包含文件即可。

include 和 require 的区别

* require 一般放在 PHP 文件的最前面，程序在执行前就会先导入要引用的文件；
* include 一般放在程序的流程控制中，当程序执行时碰到才会引用，简化程序的执行流程。
* require 引入的文件有错误时，执行会中断，并返回一个致命错误；
* include 引入的文件有错误时，会继续执行，并返回一个警告。

```php
<html>
<head>
<meta charset="utf-8">
<title>dugu</title>
</head>
<body>

<?php include 'header.php'; ?>
<h1>欢迎来到主页!</h1>
<p>一个段落文本</p>

</body>
</html>
```

## PHP 文件处理

`fopen()` 函数用于在 PHP 中打开文件。

```php
<html>
<body>

<?php
$file=fopen("test.txt","r");
?>

</body>
</html>
```

模式|	描述
-|-
r|	只读。在文件的开头开始。
r+|	读/写。在文件的开头开始。
w|	只写。打开并清空文件的内容；如果文件不存在，则创建新文件。
w+|	读/写。打开并清空文件的内容；如果文件不存在，则创建新文件。
a|	追加。打开并向文件末尾进行写操作，如果文件不存在，则创建新文件。
a+|	读/追加。通过向文件末尾写内容，来保持文件内容。
x|	只写。创建新文件。如果文件已存在，则返回 FALSE 和一个错误。
x+|	读/写。创建新文件。如果文件已存在，则返回 FALSE 和一个错误。

**PHP 文件上传**

```php
<html>
<head>
<meta charset="utf-8">
<title>菜鸟教程(runoob.com)</title>
</head>
<body>

<form action="upload_file.php" method="post" enctype="multipart/form-data">
    <label for="file">文件名：</label>
    <input type="file" name="file" id="file"><br>
    <input type="submit" name="submit" value="提交">
</form>

</body>
</html>
```

## PHP Cookie

cookie 常用于识别用户。cookie 是一种服务器留在用户计算机上的小文件。每当同一台计算机通过浏览器请求页面时，这台计算机将会发送 cookie。通过 PHP，能够创建并取回 cookie 的值。

```php
<?php
setcookie("user", "runoob", time()+3600);
?>
<html>
```

取回cookie的值

```php
<?php
// 输出 cookie 值
echo $_COOKIE["user"];

// 查看所有 cookie
print_r($_COOKIE);
?>
```

```php
<html>
<head>
<meta charset="utf-8">
<title>菜鸟教程(runoob.com)</title>
</head>
<body>

<?php
if (isset($_COOKIE["user"]))
    echo "欢迎 " . $_COOKIE["user"] . "!<br>";
else
    echo "普通访客!<br>";
?>

</body>
</html>
```

删除 Cookie

```php
<?php
// 设置 cookie 过期时间为过去 1 小时
setcookie("user", "", time()-3600);
?>
```

## PHP Session

PHP session 变量用于存储关于用户会话（session）的信息，或者更改用户会话（session）的设置。Session 变量存储单一用户的信息，并且对于应用程序中的所有页面都是可用的。

在计算机上操作某个应用程序时，用户打开它，做些更改，然后关闭它。这很像一次对话（Session）。计算机知道用户是谁。它清楚用户在何时打开和关闭应用程序。然而，在因特网上问题出现了：由于 HTTP 地址无法保持状态，Web 服务器并不知道用户是谁以及用户做了什么。

PHP session 解决了这个问题，它通过在服务器上存储用户信息以便随后使用（比如用户名称、购买商品等）。然而，会话信息是临时的，在用户离开网站后将被删除。如果用户需要永久存储信息，可以把数据存储在数据库中。

Session 的工作机制是：为每个访客创建一个唯一的 id (UID)，并基于这个 UID 来存储变量。UID 存储在 cookie 中，或者通过 URL 进行传导。

```php
<?php session_start(); ?>
 
<html>
<body>
 
</body>
</html>
```

存储和取回 session 变量的正确方法是使用 PHP $_SESSION 变量：

```php
<?php
session_start();
// 存储 session 数据
$_SESSION['views']=1;
?>

<?php
// 检索 session 数据
echo "浏览量：". $_SESSION['views'];
?>
```

在下面的实例中，创建了一个简单的 page-view 计数器。isset() 函数检测是否已设置 "views" 变量。如果已设置 "views" 变量，累加计数器。如果 "views" 不存在，则创建 "views" 变量，并把它设置为 1：

```php
<?php
session_start();
 
if(isset($_SESSION['views']))
{
    $_SESSION['views']=$_SESSION['views']+1;
}
else
{
    $_SESSION['views']=1;
}
echo "浏览量：". $_SESSION['views'];
?>
```

如果希望删除某些 session 数据，可以使用 unset() 或 session_destroy() 函数。

unset() 函数用于释放指定的 session 变量：

```php
<?php
session_start();
if(isset($_SESSION['views']))
{
    unset($_SESSION['views']);
}
?>
```

也可以通过调用 session_destroy() 函数彻底销毁 session：

```php
<?php
session_destroy();
?>
```

## PHP 错误处理

在 PHP 中，默认的错误处理很简单。一条错误消息会被发送到浏览器，这条消息带有文件名、行号以及描述错误的消息。

不同的错误处理方法：

* 简单的 "die()" 语句
* 自定义错误和错误触发器
* 错误报告

```php
<?php
if(!file_exists("welcome.txt"))
{
    die("文件不存在");
}
else
{
    $file=fopen("welcome.txt","r");
}
?>
```

```php
function customError($errno, $errstr)
{
    echo "<b>Error:</b> [$errno] $errstr<br>";
    echo "脚本结束";
    die();
}
```

## PHP 异常处理

异常用于在指定的错误发生时改变脚本的正常流程。

异常的规则

* 需要进行异常处理的代码应该放入 try 代码块内，以便捕获潜在的异常。
* 每个 try 或 throw 代码块必须至少拥有一个对应的 catch 代码块。
* 使用多个 catch 代码块可以捕获不同种类的异常。
* 可以在 try 代码块内的 catch 代码块中抛出（再次抛出）异常。

```php
<?php
// 创建一个有异常处理的函数
function checkNum($number)
{
    if($number>1)
    {
        throw new Exception("Value must be 1 or below");
    }
    return true;
}
 
// 触发异常
checkNum(2);
?>
```

```php
<?php
// 创建一个有异常处理的函数
function checkNum($number)
{
    if($number>1)
    {
        throw new Exception("变量值必须小于等于 1");
    }
        return true;
}
    
// 在 try 块 触发异常
try
{
    checkNum(2);
    // 如果抛出异常，以下文本不会输出
    echo '如果输出该内容，说明 $number 变量';
}
// 捕获异常
catch(Exception $e)
{
    echo 'Message: ' .$e->getMessage();
}
?>
```

创建一个自定义的 Exception 类

```php
<?php
class customException extends Exception
{
    public function errorMessage()
    {
        // 错误信息
        $errorMsg = '错误行号 '.$this->getLine().' in '.$this->getFile()
        .': <b>'.$this->getMessage().'</b> 不是一个合法的 E-Mail 地址';
        return $errorMsg;
    }
}
 
$email = "someone@example...com";
 
try
{
    // 检测邮箱
    if(filter_var($email, FILTER_VALIDATE_EMAIL) === FALSE)
    {
        // 如果是个不合法的邮箱地址，抛出异常
        throw new customException($email);
    }
}
 
catch (customException $e)
{
//display custom message
echo $e->errorMessage();
}
?>
```

set_exception_handler() 函数可设置处理所有未捕获异常的用户定义函数。

```php
<?php
function myException($exception)
{
    echo "<b>Exception:</b> " , $exception->getMessage();
}
 
set_exception_handler('myException');
 
throw new Exception('Uncaught Exception occurred');
?>
```

## PHP过滤器

如需过滤变量，请使用下面的过滤器函数之一：

* filter_var() - 通过一个指定的过滤器来过滤单一的变量
* filter_var_array() - 通过相同的或不同的过滤器来过滤多个变量
* filter_input - 获取一个输入变量，并对它进行过滤
* filter_input_array - 获取多个输入变量，并通过相同的或不同的过滤器对它们进行过滤

```php
<?php
$int = 123;
 
if(!filter_var($int, FILTER_VALIDATE_INT))
{
    echo("不是一个合法的整数");
}
else
{
    echo("是个合法的整数");
}
?>
```

有两种过滤器：

Validating 过滤器：

* 用于验证用户输入
* 严格的格式规则（比如 URL 或 E-Mail 验证）
* 如果成功则返回预期的类型，如果失败则返回 FALSE
  
Sanitizing 过滤器：

* 用于允许或禁止字符串中指定的字符
* 无数据格式规则
* 始终返回字符串

```php
<?php
$var=300;
 
$int_options = array(
    "options"=>array
    (
        "min_range"=>0,
        "max_range"=>256
    )
);
 
if(!filter_var($var, FILTER_VALIDATE_INT, $int_options))
{
    echo("不是一个合法的整数");
}
else
{
    echo("是个合法的整数");
}
?>
```

过滤多个输入

```php
<?php
$filters = array
(
    "name" => array
    (
        "filter"=>FILTER_SANITIZE_STRING
    ),
    "age" => array
    (
        "filter"=>FILTER_VALIDATE_INT,
        "options"=>array
        (
            "min_range"=>1,
            "max_range"=>120
        )
    ),
    "email"=> FILTER_VALIDATE_EMAIL
);
 
$result = filter_input_array(INPUT_GET, $filters);
 
if (!$result["age"])
{
    echo("年龄必须在 1 到 120 之间。<br>");
}
elseif(!$result["email"])
{
    echo("E-Mail 不合法<br>");
}
else
{
    echo("输入正确");
}
?>
```

使用 Filter Callback。通过使用 FILTER_CALLBACK 过滤器，可以调用自定义的函数，把它作为一个过滤器来使用。这样，就拥有了数据过滤的完全控制权。

```php
<?php
function convertSpace($string)
{
    return str_replace("_", ".", $string);
}
 
$string = "www_runoob_com!";
 
echo filter_var($string, FILTER_CALLBACK,
array("options"=>"convertSpace"));
?>
```

检测一个数字是否在一个范围内

```php
<?php
$int = 122;
$min = 1;
$max = 200;

if (filter_var($int, FILTER_VALIDATE_INT, array("options" => array("min_range"=>$min, "max_range"=>$max))) === false) {
    echo("变量值不在合法范围内");
} else {
    echo("变量值在合法范围内");
}
?>
```

检测 IPv6 地址

```php
<?php
$ip = "2001:0db8:85a3:08d3:1319:8a2e:0370:7334";

if (!filter_var($ip, FILTER_VALIDATE_IP, FILTER_FLAG_IPV6) === false) {
    echo("$ip 是一个 IPv6 地址");
} else {
    echo("$ip 不是一个 IPv6 地址");
}
?>
```

检测 URL - 必须包含QUERY_STRING（查询字符串）

```php
<?php
$url = "http://www.baidu.com";

if (!filter_var($url, FILTER_VALIDATE_URL, FILTER_FLAG_QUERY_REQUIRED) === false) {
    echo("$url 是一个合法的 URL");
} else {
    echo("$url 不是一个合法的 URL");
}
?>
```

移除 ASCII 值大于 127 的字符

```php
<?php
$str = "<h1>Hello WorldÆØÅ!</h1>";

$newstr = filter_var($str, FILTER_SANITIZE_STRING, FILTER_FLAG_STRIP_HIGH);
echo $newstr;
?>
```

## PHP JSON

函数|	描述
-|-
json_encode|	对变量进行 JSON 编码
json_decode|	对 JSON 格式的字符串进行解码，转换为 PHP 变量
json_last_error|	返回最后发生的错误

```php
<?php
   $arr = array('a' => 1, 'b' => 2, 'c' => 3, 'd' => 4, 'e' => 5);
   echo json_encode($arr);
?>
```

```php
<?php
   class Emp {
       public $name = "";
       public $hobbies  = "";
       public $birthdate = "";
   }
   $e = new Emp();
   $e->name = "sachin";
   $e->hobbies  = "sports";
   $e->birthdate = date('m/d/Y h:i:s a', "8/5/1974 12:20:03 p");
   $e->birthdate = date('m/d/Y h:i:s a', strtotime("8/5/1974 12:20:03"));

   echo json_encode($e);
?>
```

解析json

```php
<?php
   $json = '{"a":1,"b":2,"c":3,"d":4,"e":5}';

   var_dump(json_decode($json));
   var_dump(json_decode($json, true));
?>
```

以上代码执行结果为：

```php
object(stdClass)#1 (5) {
    ["a"] => int(1)
    ["b"] => int(2)
    ["c"] => int(3)
    ["d"] => int(4)
    ["e"] => int(5)
}

array(5) {
    ["a"] => int(1)
    ["b"] => int(2)
    ["c"] => int(3)
    ["d"] => int(4)
    ["e"] => int(5)
}
```
