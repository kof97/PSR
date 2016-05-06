翻译自：
> https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md

---
# 自动载入
---
## 1. 概述
这个 PSR 描述的是通过文件路径自动载入类的指南，它作为对 PSR-0 的补充；根据这个来规范存放文件以实现自动载入

---
## 2. 说明 `Specification`
1. 术语 `class` 包含类 `class`，接口 `interface`，特性 `traits` 以及其他一些类似的结构

2.  一个完整的限定类名应该按照如下范例：
    `\<NamespaceName>(\<SubNamespaceNames>)*\<ClassName>`
    * 完整的限定类名 `必须` 有一个顶级命名空间，如 `Vendor Name`
    * 完整的限定类名 `可以` 有多个子命名空间
    * 完整的限定类名 `必须` 有一个终止的类名
    * 下划线 `_` 在完整的限定类名中没有特殊含义
    * 字母字符在完整的限定类名中 `可以` 是任何的大小写组合
    * 所有的类名 `必须` 以大小写敏感的方式引入    

3. 当通过一个完整的限定类名引入一个文件时：
    * 连续的一个或几个子命名空间构成的 `命名空间前缀`（不包括顶级命名空间的分隔符），在完整的限定类名中，至少对应着至少一个 `基础目录` 
（译者注：也就是说 `命名空间前缀` 要对应着一个 `基础目录`）

    * 在 `命名空间前缀` 后的连续的 `子命名空间`名称对应着 `基础目录` 下的 `子目录`，其中的 `命名空间分隔符` 表示 `目录分隔符`，`子目录名称` 必须和 `子命名空间名` 大小写匹配
（译者注：也就是说，各个 `子命名空间` 对应着各个 `子目录`，并且名称与子目录相同，大小写匹配）

    * 终止类名对应一个以 `.php` 结尾的文件，`文件名` `必须` 和 `终止类名` 大小写匹配

4. 自动载入器 `不可` 抛出任何异常，`不可` 引发任何等级的错误；也 `不应该` 返回任何值；

---
## 3. 示例
如下表格展示的是与 `完整的限定类名`、`命名空间前缀` 和 `基础目录` 对应的 `文件路径`

| 完整的限定类名 | 命名空间前缀 | 基础目录 | 实际文件路径 |
|----------   |            |        |            |
| \Acme\Log\Writer\File_Writer | Acme\Log\Writer | ./acme-log-writer/lib/ | ./acme-log-writer/lib/File_Writer.php |
| \Aura\Web\Response\Status | Aura\Web | /path/to/aura-web/src/ | /path/to/aura-web/src/Response/Status.php |
| \Symfony\Core\Request | Symfony\Core | ./vendor/Symfony/Core/ | ./vendor/Symfony/Core/Request.php |
| \Zend\Acl | Zend | /usr/includes/Zend/ | /usr/includes/Zend/Acl.php |


