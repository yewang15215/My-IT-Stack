# PHP

## 基础
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