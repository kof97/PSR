翻译自 
> https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md

# 基本代码规范
## 1、概述
> * `必须` 使用 `<?php ?>` 或是 `<?= ?>` 这两种标签
> * PHP 代码中 `必须` 使用 `UTF-8 without BOM` 编码方式
> * 每个文件 `建议` 只用来声明（类 `class`，函数 `function`，常量 ` constant` 等） 或者只用来做一些辅助操作（输出信息，修改配置等），但是一个文件 `不建议` 同时做这两件事
> * 命名空间 `Namespace` 和类 `class` `必须` 遵循"autoloading" PSR标准: [PSR-0, PSR-4].
> * 类名（`class`）`必须` 使用大驼峰命名法，如 `StudlyCaps`
> * 类中的常量 `必须` 只能用 `大写字母` 和 `_` 来命名
> * 方法名（`method`）`必须` 使用驼峰命名法，如 `camelCase`

## 2、文件
### 2.1. PHP 标签
PHP 代码中 `必须` 使用 `<?php ?>` 或者 `<?= ?>`，而不可使用其他标签

### 2.2. 字符编码
PHP 代码 `必须` 使用 `UTF-8 without BOM` 编码

### 2.3 Side Effects（译者注：可理解为辅助操作，其他操作，副操作）
每个文件 `建议` 只用来声明（类 `class`，函数 `function`，常量 ` constant` 等） 或者只用来做一些辅助操作（输出信息，修改配置等），但是一个文件 `不建议` 同时做这两件事

`side effects` 的意思可以理解为：在包含文件时，执行的逻辑操作与所声明的类(class)，函数(function)，常量(constant)等没有直接的关系

`side effects` 可以包含这些操作但并不局限于此：输出信息，显式地使用 `require` 或 `include`，连接外部服务，修改 `ini` 配置，触发错误或异常，修改全局或者静态变量，读取或写入文件等等

下面是一个同时拥有声明和 `side effects` 的例子，应该避免：
``` php
<?php
// side effect: change ini settings
ini_set('error_reporting', E_ALL);

// side effect: loads a file
include "file.php";

// side effect: generates output
echo "<html>\n";

// declaration
function foo()
{
    // function body
}
```
这是一个只包含声明的例子，应该建议的方式：
``` php
<?php
// declaration
function foo()
{
    // function body
}

// conditional declaration is *not* a side effect
if (! function_exists('bar')) {
    function bar()
    {
        // function body
    }
}
```  

## 3、命名空间 namespace 和类名 class name   

命名空间 `Namespace` 和类 `class` `必须` 遵循"autoloading" PSR标准: [PSR-0, PSR-4].

这意味着每个文件中只能有一个类 `class`，并且每个类 `class` 至少要有一级命名空间 `namespace`：即一个顶级的 `vendor name`

类名（`class`）`必须` 使用大驼峰命名法，如 `StudlyCaps`

`PHP5.3` 之后的 `必须` 使用正式的命名空间 `namespace`，例：  

``` php
<?php
// PHP 5.3 and later:
namespace Vendor\Model;

class Foo
{
}
```  

`PHP5.2.x` 和之前的版本 `建议` 用伪命名空间 `Vendor_` 作为类名的前缀  

``` php
<?php
// PHP 5.2.x 及之前:
class Vendor_Model_Foo
{
}
```  

## 4、类的常量 constant、属性 property、方法 method

类 `class` 指所有的类 `class`，接口 `interface` 和特性 `trait`

### 4.1. 常量 `constant`  

类中的常量 `必须` 只能用 `大写字母` 和 `_` 来命名，例：  

``` php
<?php
namespace Vendor\Model;

class Foo
{
    const VERSION = '1.0';
    const DATE_APPROVED = '2012-06-01';
}
```  

### 4.2. 属性 property 

这个指南中不再对 `StudlyCaps`，`$camelCase` 或是 `$unser_score` 中的某一个风格做特别推荐，由个人喜好而定

但不管你如何定义，都 `建议` 在一定范围内保持风格的一致，这个范围 `可能` 是 `vendor`，`package`，`class`，或者 `method`

### 4.3. 方法 method  

方法名（`method`）`必须` 使用驼峰命名法，如 `camelCase`