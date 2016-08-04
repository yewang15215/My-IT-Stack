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


### 调试
* 调试器
    - PHP 5.6 带来了 [phpdbg 交互式调试器](http://php.net/manual/zh/migration56.new-features.php#migration56.new-features.phpdbg)
    - [Zend IDE](http://www.zend.com/en/products/studio/) 的调试器
    - [DBG](http://www.php-debugger.com/dbg/)
    - [APD](http://pecl.php.net/apd)
    - [Xdebug](http://xdebug.org/)

### 包管理器
* composer
    - 安装  
        `curl -sS https://getcomposer.org/installer | php`  
        `mv composer.phar /usr/local/bin/composer`

### PHP 库
* log
    - [monolog](https://github.com/Seldaek/monolog)

### REPL
* [boris](https://github.com/borisrepl/boris)
* [psysh](https://github.com/bobthecow/psysh)

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