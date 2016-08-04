# Vagrant

### 修改vagrant box 的名称
使用`vagrant box list` 可以查看当前系统添加的**box 列表**，要修改其中某个box 的名称：
`mv vagrant-path/boxes/box-def-name vagrant-path/boxes/new-box-def-name`，
然后修改使用该box 创建的系统的**Vagrantfile 文件**，把`config.vm.box="box-def-name"` 改为`config.vm.box="new-box-def-name"`。
vagrant-path 一般是path-to-your-home/.vagrant.d。
<!-- more --> 
### 查看box 的下载路径
国内直接vagrant add/init 官方远程库的速度往往很慢，于是很多时候都需要把box 下载到本地，然后add。有时候在github 看上一个想要的box，但是教程里没有提到box 的下载路径，就需要自己去查询了。
比如[scotch-box](https://github.com/scotch-io/scotch-box)，教程只提到了直接`git clone` 他的项目，然后`vagrant up`，就可以自动下载并开启系统了。
现在我们想把box 下载的本地：
先进[vagrantcloud](https://vagrantcloud.com/)，然后搜索`scotch box`，第一个就是[scotch-box](https://atlas.hashicorp.com/scotch/boxes/box) 了，进去可以看到作者上传的每个版本，然后我们就可以拼接我们需要的box 的下载地址：
box 所在地址 + `versions` + 在每个版本的右上角会看到的版本号 + `providers` + 虚拟机类型 + `.box`。
比如我需要的box 下载链接就是这样的：
`https://atlas.hashicorp.com/scotch/boxes/box/versions/2.5/providers/virtualbox.box`

3. Windows 下，box 下载路径与当前命令路径**不在一个盘**，怎么样构造`box-url`
我们知道，当box 下载到本地，可以使用`vagrant box add box-def-name box-url` 把box 添加到当前系统，会在`vagrant-path/boxes` 下生成**对应虚拟机类型**的版本。
最简单的方法是直接进入到**box 下载路径下**，然后运行`vagrant box add box-def-name box-name` 即可，而在同一个盘下面，也可以使用相对路径来构造`box-url`。
但如果不进入box 所在的盘，也可以直接构造box-url：
`file:///盘符:/your-box-path/box-name.box`。

4. 一些常用的`vagrant 命令`
* vagrant box
`vagrant box add box`(官方名字)
`vagrant box add box-def-name box-url`
`vagrant box list`
`vagrant box remove`
* vagrant init
进入所要生成项目的路径下执行`vagrant init`,**Vagrantfile**
`vagrant init box-def-name` ，相当于执行`vagrant init`，然后修改**Vagrantfile**，`config.vm.box = "centos-6.6"`。
* vagrant up 
* vagrant ssh
* vagrant halt 
* vagrant reload
* vagrant suspend
* vagrant resume
* vagrant status
* vagrant ssh-config
* vagrant destroy
* vagrant package
* vagrant plugin
* vagrant provision
5. [将Vagrant 移出系统盘](http://wing2south.com/post/44371306891/vagrant/)