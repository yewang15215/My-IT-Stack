# PHP

## 基础

### 编程规范
#### 命名规范
* 全局变量
    - `$g_` 开头
* 一般变量
    - 小写字母、下划线
* 临时变量
    - 临时变量如$i、$j 等仅用于循环中，不要作其他用途
* 函数
    - 小写字母、下划线、动词+名词
    - 完成一组功能的函数放到一个文件中，存放函数的文件采用function_name.func.php命名
* 类
    - 首字母大写、包括首个单词
    - 在类中，方法放到属性定义前边、公用方法放到专用方法前边
    - 一般一个类对应到一个文件，当一些类关系紧密时，可以存放在一个文件中
    - 存放类的文件采用ClassName.class.php方式命名
* 方法
    - 首个单词小写，其余单词的首字母大写
    - 不要采用不常用的缩写
    - 使用常用的缩写时，只大写首字母

#### 板式规则
* 语义分隔
    - 各个函数、方法之间应该采用空行间隔
    - 同一个函数中联系紧密的语句之间可以不换行，其他情况需要换行


### 计算日期差
* 方法一
```
$dayBegin = "2016-07-23";
$daysDiff = (strtotime(date("y-m-d")) - strtotime($dayBegin)) / 86400;
```
* 方法二
```
$dayBegin = "2016-07-23";
$interval = (new DateTime())->diff(new DateTime($dayBegin));
$daysDiff = $interval->days;
```

### 魔术常量
```
__LINE__    文件中的当前行号。
__FILE__    文件的完整路径和文件名。如果用在被包含文件中，则返回被包含的文件名。自 PHP 4.0.2 起，__FILE__ 总是包含一个绝对路径（如果是符号连接，则是解析后的绝对路径），而在此之前的版本有时会包含一个相对路径。
__DIR__     文件所在的目录。如果用在被包括文件中，则返回被包括的文件所在的目录。它等价于 dirname(__FILE__)。除非是根目录，否则目录中名不包括末尾的斜杠。（PHP 5.3.0中新增） =
__FUNCTION__    函数名称（PHP 4.3.0 新加）。自 PHP 5 起本常量返回该函数被定义时的名字（区分大小写）。在 PHP 4 中该值总是小写字母的。
__CLASS__   类的名称（PHP 4.3.0 新加）。自 PHP 5 起本常量返回该类被定义时的名字（区分大小写）。在 PHP 4 中该值总是小写字母的。类名包括其被声明的作用区域（例如 Foo\Bar）。注意自 PHP 5.4 起 __CLASS__ 对 trait 也起作用。当用在 trait 方法中时，__CLASS__ 是调用 trait 方法的类的名字。
__TRAIT__   Trait 的名字（PHP 5.4.0 新加）。自 PHP 5.4 起此常量返回 trait 被定义时的名字（区分大小写）。Trait 名包括其被声明的作用区域（例如 Foo\Bar）。
__METHOD__  类的方法名（PHP 5.0.0 新加）。返回该方法被定义时的名字（区分大小写）。
__NAMESPACE__   当前命名空间的名称（区分大小写）。此常量是在编译时定义的（PHP 5.3.0 新增）。
```

### 魔术方法
```
__construct()， 
__destruct()， 
__call()， 
__callStatic()， 
__get()， 
__set()， 
__isset()， 
__unset()， 
__sleep()， 
__wakeup()，
__toString()， 
__invoke()， 
__set_state()， 
__clone(),
__debugInfo() 
等方法在 PHP 中被称为"魔术方法"（Magic methods）。
在命名自己的类方法时不能使用这些方法名，除非是想使用其魔术功能。
```
### 自动加载
* `spl_autoload_register` — 注册给定的函数作为 `__autoload` 的实现


### 修改时区
* 修改PHP.ini  
  date.timezone = Asia/Shanghai
* 修改 .htaccess  
  php_value date.timezone Asia/Shanghai  
  或  
  SetEnv TZ Asia/Shanghai
* 在PHP 代码中添加
  `date_default_timezone_set('Asia/Shanghai');`  
  或  
  `ini_set('date.timezone','Asia/Shanghai');`

### 语法
* namespace 与 use
* 字符串替换
    - strtr(string,from,to)
    - mixed str_replace ( mixed $search , mixed $replace , mixed $subject [, int &$count ] )
        + mixed 说明一个参数可以接受多种不同的（但不一定是所有的）类型。
        + 例如 gettype() 可以接受所有的 PHP 类型，str_replace() 可以接受字符串和数组。
    - mixed preg_replace ( mixed $pattern , mixed $replacement , mixed $subject [, int $limit = -1 [, int &$count ]] )
* print_r 与 var_dump 的区别
* json_encode
* json_decode
    - 参数必须是对象（object）和数组（array）
    - json的分隔符（delimiter）只允许使用双引号
    - json名值对的"名"（冒号左边的部分），任何情况下都必须使用双引号。
* 大小写问题
    - 变量名**区分**大小写
    - 常量名*默认* **区分**大小写，通常为大写
    - php.ini 配置项**区分**大小写
    - 函数名、方法名、类名**不区分**大小写


### 防止SQL 注入
* 使用[PDO](http://php.net/manual/zh/book.pdo.php) (PHP Data Objects)
``` php
$stmt = $pdo->prepare('SELECT * FROM employees WHERE name = :name');

$stmt->execute(array('name' => $name));

foreach ($stmt as $row) {
    // do something with $row
}
```

* 使用[MySQLi](http://php.net/manual/zh/book.mysqli.php) (MySQL Improved Extension)
```
$stmt = $dbConnection->prepare('SELECT * FROM employees WHERE name = ?');
$stmt->bind_param('s', $name);

$stmt->execute();

$result = $stmt->get_result();
while ($row = $result->fetch_assoc()) {
    // do something with $row
}
```


## 调试
* 调试器
    - PHP 5.6 带来了 [phpdbg 交互式调试器](http://php.net/manual/zh/migration56.new-features.php#migration56.new-features.phpdbg)
    - [Zend IDE](http://www.zend.com/en/products/studio/) 的调试器
    - [DBG](http://www.php-debugger.com/dbg/)
    - [APD](http://pecl.php.net/apd)
    - [Xdebug](http://xdebug.org/)

## 包管理器
* composer
    - 安装  
        `curl -sS https://getcomposer.org/installer | php`  
        `mv composer.phar /usr/local/bin/composer`

## PHP 库
* log
    - [monolog](https://github.com/Seldaek/monolog)

## REPL
* [boris](https://github.com/borisrepl/boris)
* [psysh](https://github.com/bobthecow/psysh)