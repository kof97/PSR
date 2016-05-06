# 代码风格指南
---
翻译自：
> https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md

PSR-2 在 PSR-1 的基础上进行了继承和扩展

---
## 1. 概述
> * 代码 `必须` 遵循 `PSR-1` 规范
> * 代码 `必须` 使用 `4个空格` 的缩进，而不是制表符 `tab`
> * 一行代码长度 `不可` 有硬性限制，软限制必须为120个字符，也应当是80个字符或者更少
> * 在 `namespace` 声明下面 `必须` 有一个空行，并且 `use` 声明代码块下面也必须有一个空行
> * 类的开始花括号 `必须` 放到下一行，结束花括号 `必须` 放在类主体的下一行
> * 方法的开始花括号 `必须` 放在下一行，结束花括号 `必须` 放在方法主体下面
> * 所有的属性和方法的可见性 `必须` 显式(译者注：`Public`, `Protect`, `Private`)声明，`abstract` 和 `final` 声明必须在显式声明可见性之前，`static` 声明必须在显式声明可见性之后
> * 控制结构（译者注：`for`，`while` 等）的关键词 `必须` 在后面有一个空格； 方法和函数 `必须` 没有
> * 控制结构（译者注：`for`，`while` 等）的开始花括号 `必须` 放在同一行，结束花括号 `必须` 放在控制主体的下一行
> * 控制结构的左括号后面不可有空格，右括号之前不可有空格

### 1.1. 示例
对于上述规则的一些示例：

``` php
<?php
namespace Vendor\Package;

use FooInterface;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class Foo extends Bar implements FooInterface
{
    public function sampleFunction($a, $b = null)
    {
        if ($a === $b) {
            bar();
        } elseif ($a > $b) {
            $foo->bar($arg1);
        } else {
            BazClass::bar($arg2, $arg3);
        }
    }

    final public static function bar()
    {
        // method body
    }
}
```
---
## 2. 常规
### 2.1 基础编码规范
代码 `必须` 遵守 `PSR-1` 的所有规范

### 2.2 文件
所有的 PHP 文件 `必须` 使用 `Unix LF` (换行)作为行结束符

所有PHP文件 `必须` 以一个空行结束

只有 PHP 代码的文件关闭标签 `?>` `必须` 省略

### 2.3 行
每行的长度 `不可` 有硬性限制

每行长度的软限制必须是 `120` 个字符，对于软限制，自动样式检查器 `必须` 警告但 `不可` 报错

每行实际长度 `不应该` 超过 `80` 个字符，较长的行 `应该` 被拆分成多个不超过 `80` 个字符的后续行

在非空行后面 `不可` 有空格

空行 `可以` 用来改善可读性和区分相关的代码块

每行 `不可` 多于一个语句

### 2.4 缩进
代码 `必须` 使用 `4个空格` 的缩进，并且 `不可` 使用制表符 `tab` 作为缩进
> 注意：只用空格，不与制表符 `tab` 混合使用，将会对避免代码差异，补丁，历史和注解中的一些问题有帮助。使用空格还可以使调整细微的缩进来改进行间对齐变得简单

### 2.5 关键词 `keywords` 和 `True/False/Null`
PHP 的关键词 `keywords` `必须` 用小写

PHP 中的常量 `true`，`false`，`null` `必须` 全部小写

---
## 3. `Namespace` 和 `Use` 声明
如果存在，`namespace` 声明后面 `必须` 有一个空行

如果存在，所有的 `use` 声明 `必须` 放在 `namespace` 声明下面

一个 `use` 关键字 `必须` 只用于一个声明

`use` 声明代码块后面 `必须` 有一个空行

例：
``` php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

// ... additional PHP code ...
```
---
## 4. 类 `class`，属性 `property`，方法 `method`
类 `class` 指所有的类 `class`，接口 `interface` 和特性 `trait`

### 4.1. 继承 `extends` 和接口实现 `implements`
一个类的 `extends` 和 `implements` 关键词 `必须` 和类名 `class name` 在同一行

类的开始花括号 `必须` 放在下面自成一行，结束花括号 `必须` 放在类主体的后面自成一行
``` php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements \ArrayAccess, \Countable
{
    // constants, properties, methods
}
```

接口实现 `implements` 的列表 `可以` 被拆分为多个有一次缩进的后续行。如果这么做，接口列表的第一个接口名 `必须` 要放在下一行，并且每行 `必须` 只有一个接口。
``` php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements
    \ArrayAccess,
    \Countable,
    \Serializable
{
    // constants, properties, methods
}
```

### 4.2. 属性 `property`
所有的属性 `必须` 显式声明可见性

`var` 关键词 `不可` 用来声明属性

一个语句 `不可` 声明多个属性

属性名称 `不应该` 使用单个下划线作为前缀来表明保护或私有的可见性

一个属性声明应该像这样：
``` php
<?php
namespace Vendor\Package;

class ClassName
{
    public $foo = null;
}
```

### 4.3. 方法 `method`
所有的方法 `必须` 显式声明可见性

方法名 `不应该` 使用单个下划线作为前缀来表明保护或私有的可见性

方法名在声明之后 `不可` 跟随一个空格。开始花括号 `必须` 放在下面自成一行，并且结束花括号 `必须` 放在方法主体的下面自成一行

左括号后面 `不可` 有空格，右括号前面 `不可` 有空格

一个方法定义应该像下面这样， 注意括号，逗号，空格和花括号：
``` php
<?php
namespace Vendor\Package;

class ClassName
{
    public function fooBarBaz($arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}
```

### 4.4. 方法参数 `Method Arguments`
参数列表中，逗号之前 `不可` 有空格，逗号之后 `必须` 要有一个空格

方法中有默认值的参数 `必须` 放在参数列表的最后面
``` php
<?php
namespace Vendor\Package;

class ClassName
{
    public function foo($arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}
```
参数列表 `可以` 被分为多个有一次缩进的多个后续行。如果这么做，列表的第一项 `必须` 放在下一行，并且每行 `必须` 只放一个参数

当参数列表被分为多行，右括号和左花括号 `必须` 夹带一个空格放在一起自成一行
``` php
<?php
namespace Vendor\Package;

class ClassName
{
    public function aVeryLongMethodName(
        ClassTypeHint $arg1,
        &$arg2,
        array $arg3 = []
    ) {
        // method body
    }
}
```

### 4.5. `abstract`，`final` 和 `static`
如果存在，`abstract` 和 `final` 声明 `必须` 放在可见性声明之前

如果存在，`static` 声明 `必须` 放在可见性声明后一个
``` php
<?php
namespace Vendor\Package;

abstract class ClassName
{
    protected static $foo;

    abstract protected function zim();

    final public static function bar()
    {
        // method body
    }
}
```

### 4.6. 方法 `method` 和函数 `function` 调用
当进行函数或方法调用的时候，在方法或者函数名与左括号之间 `不可` 有空格，左括号之后 `不可` 有空格，右括号之前 `不可` 有空格

参数列表中，逗号之前 `不可` 有空格，逗号之后 `必须` 有一个空格
``` php
<?php
bar();
$foo->bar($arg1);
Foo::bar($arg2, $arg3);
```

参数列表 `可以` 被拆分成多个有一个缩进的后续行。如果这么做，列表中的第一项 `必须` 放在下一行，并且每一行 `必须` 只有一个参数
``` php
<?php
$foo->bar(
    $longArgument,
    $longerArgument,
    $muchLongerArgument
);
```
---
## 5. 控制结构 `Control Structures`
对于控制结构通常的样式规则如下：

> * 控制结构关键词之后 `必须` 有一个空格
> * 左括号之后 `不可` 有空格
> * 右括号之前 `不可` 有空格
> * 在右括号和开始花括号之间 `必须` 有一个空格
> * 代码主体 `必须` 有一次缩进
> * 结束花括号 `必须` 在主体的下一行

结构的主体部分 `必须` 被括在花括号里，这使结构体看起来更加标准，减少了在主体部分中加入新行时出现错误的可能

### 5.1. `if`，`elseif`，`else`
一个 `if` 结构看起来应该像下面这样。注意括号，空格，花括号的位置，并且 `else` 和 `elseif` 和前一个主体的结束花括号在同一行
``` php
<?php
if ($expr1) {
    // if body
} elseif ($expr2) {
    // elseif body
} else {
    // else body;
}
```
关键词 `elseif` `应该` 替代 `else if`，以保持所有的控制关键词像一个单词

### 5.2. `switch`，`case`
一个 `switch` 结构看起来应该像下面这样。注意括号，空格和花括号。`case` 语句必须从 `switch` 处缩进，并且 `break` 关键字（或其他中止关键字）必须和 `case` 主体缩进在同级。如果一个非空的 `case` 主体往下落空（译者注：就是这个 `case` 不适用 `break` 结束）则必须有一个类似 `// no break` 的注释
``` php
<?php
switch ($expr) {
    case 0:
        echo 'First case, with a break';
        break;
    case 1:
        echo 'Second case, which falls through';
        // no break
    case 2:
    case 3:
    case 4:
        echo 'Third case, return instead of break';
        return;
    default:
        echo 'Default case';
        break;
}
```

### 5.3. `while`，`do while`
一个 `while` 语句看起来应该像下面这样。注意括号，空格和花括号的位置
``` php
<?php
while ($expr) {
    // structure body
}
```
相同的，一个 `do while` 语句看起来应该像下面这样。注意括号，空格和花括号的位置
``` php
<?php
do {
    // structure body;
} while ($expr);
```

### 5.4. `for`
一个 `for` 语句看起来应该像下面这样。注意括号，空格和花括号的位置
``` php
<?php
for ($i = 0; $i < 10; $i++) {
    // for body
}
```

### 5.5. `foreach`
一个 `foreach` 语句看起来应该像下面这样。注意括号，空格和花括号的位置
``` php
<?php
foreach ($iterable as $key => $value) {
    // foreach body
}
```

### 5.6. `try`，`catch`
一个 `try catch` 语句看起来应该像下面这样。注意括号，空格和花括号的位置
``` php
<?php
try {
    // try body
} catch (FirstExceptionType $e) {
    // catch body
} catch (OtherExceptionType $e) {
    // catch body
}
```
---
## 6. 闭包 `Closures`
闭包在声明时 `function` 关键词之后 `必须` 有一个空格，并且 `use` 之前也需要一个空格

开始花括号 `必须` 与 `function` 在同一行，结束花括号 `必须` 在主体的下一行

参数列表和变量列表的左括号之后 `不可` 有空格，其右括号之前也 `不可` 有空格

在参数列表和变量列表中，逗号之前 `不可` 有空格，逗号之后 `必须` 有空格

闭包带默认值的参数 `必须` 放在参数列表后面

一个闭包声明看起来应该像下面这样。注意括号，空格和花括号的位置
``` php
<?php
$closureWithArgs = function ($arg1, $arg2) {
    // body
};

$closureWithArgsAndVars = function ($arg1, $arg2) use ($var1, $var2) {
    // body
};
```
参数和变量列表 `可以` 被分成多个带一次缩进的后续行。如果这么做，列表的第一项 `必须` 放在下一行，并且一行 `必须` 只放一个参数或变量

当最终列表（不管是参数还是变量）被分成多行，右括号和开始花括号 `必须` 夹带一个空格放在一起自成一行。

下面是一个参数和变量列表被分割成多行的示例：
``` php
<?php
$longArgs_noVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) {
   // body
};

$noArgs_longVars = function () use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};

$longArgs_longVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};

$longArgs_shortVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use ($var1) {
   // body
};

$shortArgs_longVars = function ($arg) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};
```
注意如果在函数或者方法中把闭包作为一个参数调用，上面的样式规则也适用
``` php
<?php
$foo->bar(
    $arg1,
    function ($arg2) use ($var1) {
        // body
    },
    $arg3
);
```
---
## 7. 结论
该指南中有很多风格的元素和做法被故意忽略掉。这些包括下面的等等：
> * 全局变量和全局常量的声明
> * 方法声明
> * 操作符和赋值
> * 行间对齐
> * 注释和文档块
> * 类名给你前缀和后缀
> * 最佳实践

---
> 敲了快两个小时。。要疯了（生无可恋）。。