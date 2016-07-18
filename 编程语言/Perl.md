# Perl

## 基础
* 读取文件
    - 整体读入，逐行处理  
    ``` perl
    open(FILE,"<","/home/chenmi/.bashrc")||die"cannot open the file: $!\n";
    @linelist=<FILE>;
    foreach $eachline(@linelist){
        print $eachline;
    }
    close FILE;
    ```
    - 逐行读入，边读边处理  
    ``` perl
    open(FILE,"<","/home/chenmi/.bashrc")||die"cannot open the file: $!\n";
    while (<FILE>){
        print;
    }
    close FILE;
    ```
    - 第一种方法适合于较小的文件，一次全部读入到array 之后可以更加灵活的处理;第二种方法则适合于大型文件，一次读入一行，可以减少内存占用。

## REPL
* 模拟REPL
    - `perl -de1`