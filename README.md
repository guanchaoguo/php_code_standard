| 版本号  | 编写人员 | 编写时间  | 备注  |
| ------------ | ------------ | ------------ | ------------ |
| v0.1  | ---  | -----  ------| ------------ |--------------|
[TOC]

# 1. 编写目的
> 为了更好的提高技术部的工作效率，保证开发的有效性和合理性，并可最大程度的提高程序代码的可读性和可重复利用性，指定此规范。开发团队根据自己的实际情况，可以对本规范进行补充或裁减。
注：在使用一些框架时，如果其特定要求的一些规范与本规范部分相冲突，请以其特定要求为准

# 2. 整体要求
> PHP 开发规范将参照 PSR 的规范，基本采用 PSR 指定的规范，在其基础上增加、修改或删除部分适合具体开发环境的规范。本规范只针对 PHP 开发过程中编码的规范，对于 PHP 开发项目中文件、目录、数据库等方面的规范，将不重点涉及,必须严格按照 [PSR1-4](https://psr.phphub.org/),代码提交之前,可以用 [PHP-CS-Fixer](https://github.com/FriendsOfPHP/PHP-CS-Fixer) 工具格式化
本规范包含了 PHP 开发时程序编码中命名规范、代码缩进规则、控制结构、函数调用、函数定义、注释、包含代码、PHP标记、文件头的注释块、CVS标记、URL样例、常量命名等方面的规则.开放工具推荐使用 PHPStorm

# 3. PHP 规范
- 3.1. 代码文件必须是 <?php 开头,如果是框架和纯 PHP代码,不该 ?> 结束
- 3.2. 代码文件必须是不带BOM UTF8 编码
- 3.3. 代码文件必须用 Unix LF 作为行结束标识符(在 Windows 环境写代码需要注意下编辑器的设置)
- 3.4. 代码必须时 4 个空格,一定不可制表符
- 3.5. 代码文件必须以空白行作为结束
- 3.6. 每行代码应该控制在 120 (PHPStorm 可以设置边缘线),大于 120 的,应该折成多行
- 3.7. 每个必须只有一条语句Œ
- 3.8. PHP 所有关键字,必须是全部小写
- 3.9. 命名空间和类必须符合 PSR-4 自动加载规范,基本代码规范,必须符合 PSR-1
- 3.10. 命名空间和 use 中间必须有一个空白行,use 后面必须有空白行
- 3.11. 类,接口,Traits(可复用代码块) 的命名必须是大驼峰,以大写开头,如: ClassName
- 3.12. 类的常量必须全部大写,单词之间用下划线分隔如: CONST_NAME
- 3.13. 类和方法开始的大括号和结束的大括号必须时单独一行
- 3.14. 类的属性和方法,必须添加访问修饰符(private,protected,public),abstract 和 final 必须在访问修饰符之前,static 必须在访问修饰符之后
- 3.15. 方法必须是小驼峰,以小写开头,如 functionName,
- 3.16. 函数声明,应该用 function_exists 判断
- 3.17. 变量和类属性声明,应该用小驼峰,以小写开头,不要做没有意义缩写,如"用户 ID"必须是 "user_id",而不能是 "uid"
- 3.18. 控制结构的关键字后必须要有一个空格符,而调用方法或函数时则一定不要有,开始大括号和关键字必须同行,结束大括号必须单独一行.而且必须写大括号.
- 3.19. 控制语句,多个条件,必须用小括号括起来,elseif 必须是连在一起,不允许出现 else if

# 4. MySQL 规范
- 4.1. IP,时间,必须用 unsigned int 类型,
- 4.2. 确认是无符号的,一定要把类型改为 unsigned
- 4.3. 唯一的字段,一定要在数据库层做好唯一索引,索引以 "idx_" 开头
- 4.4. 数据库名称必须是小写字母+数字(不推荐数字),并且使用下划线"_"分割
- 4.5. 字段禁止使用 [MySQL 保留字](https://dev.mysql.com/doc/refman/8.0/en/keywords.html),长度不能长于 16 个字符,字段尽量能够简洁和见名识义
- 4.6. 临时表必须以"tmp_" 开头,备份表必须以 "bak_" 开头,日期结束,如"bak_users_2019-02-28"
- 4.7. 所有相同数据存储的字段名称,必须一致(主键除外),如 "users" 表中的 "id" (用户 ID),在下注表应该是 "user_id",账变表应该也是 "user_id",不能用简称 "uid" 类似.
- 4.8. 数据库引擎尽量是 InnoDB,如果需要用到 MEMORY 类型,建议用 Memcached 或者是 Redis 之类的存储,创建表时,不能有保留字段
- 4.9. 数据库和表必须是 utf8mb4 类型,不能用 Latin 或者时 GBK 等.并且所有的表和字段都必须备注,如果是状态类型,一定要写好每个状态的说明.
- 4.10. 文件和图片禁止直接存储数据库
- 4.11. 表尽量避免使用 TEXT,BLOB,ENUM类型,字段尽量为 NOT NULL,然后给一个 默认值,禁止使用 float 类型,需要使用 decimal 类型,尽量设置自增主键
- 4.12. 避免使用外键约束

# 5. 接口设计规范
- 5.1

# 6. 文档编写规范

1. 所有文档以 Markdown 格式,提交到 GitLab 服务器
2. 文档头必须有版本号说明 

# 7. 注释规范
## 7.1 文件头注释规范
```
 /**
 * ${FILE_NAME}
 * // 这里是注释
 * @package    ${PRODUCT_NAME}
 * @author     你的名字,昵称等
 * @date       ${YEAR}-${MONTH}-${DAY} ${HOUR}:${MINUTE}:${SECOND}
 */
如下:
 /**
    * LotteryDataLogic.php
    * 开奖数据处理
    * @package    Admin
    * @author     Channing
    * @date       2019-02-28 11:11:18
    */
```
## 7.2 方法/函数注释

```
 /**
 * 
${PARAM_DOC}
 * @author 你的名字,昵称等
 * @date   ${YEAR}-${MONTH}-${DAY} ${HOUR}:${MINUTE}:${SECOND}
#if (${TYPE_HINT} != "void") * @return ${TYPE_HINT}
#end
 */
如下:
 /**
    *
    * @param Request $request
    * @author Channing
    * @date   2019-02-28 11:11:18
    * @return void
    */
```

#技术栈:
```
MySQL 5.8.*
PHP 7.3.*
Redis 5.0.*
Nginx 1.14.*
Memcached 1.5.*
RabbitMQ 3.7.*
Laravel 5.*
Lumen 5.*

PHP 扩展
swoole 4.2.* (指定服务器)
phpredis 4.2.*
php7.3-bcmath
php7.3-fpm
php7.3-mbstring
php7.3-mysql
php7.3-xml
php7.3-zip
php7.3-curl
php7.3-dev (编译扩展需要)

```