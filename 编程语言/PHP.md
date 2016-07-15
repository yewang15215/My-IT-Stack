# PHP

## 调试
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

## 防止SQL 注入
* 使用[PDO](http://php.net/manual/zh/book.pdo.php) (PHP Data Objects)
* 使用[MySQLi](http://php.net/manual/zh/book.mysqli.php) (MySQL Improved Extension)