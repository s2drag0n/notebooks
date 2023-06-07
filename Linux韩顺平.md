[TOC]

# 韩顺平Linux

## Linux基础篇

### 内容介绍

#### 简介

基础、实操、内核、专题

linux开发、运维、嵌入式

应用领域有个人桌面、服务器领域、嵌入式领域

Linux Torvalds

#### linux和unix关系

> 上世纪70年代 贝尔实验室开发了Unix系统，80年代惠普、IBM等公司开发了各种Unix发行版。此时，Richard Stallmar指出“在自由的时代用户应该免费享有对软件源代码阅读、修改的权力，而软件公司可以靠提供服务和训练获得盈利”，所以他发起了[GNU计划](https://zh.wikipedia.org/wiki/GNU%E8%A8%88%E5%8A%83)，于是Linux Torvalds参加了GNU计划并贡献了Linux内核的第一个版本。
>
> Minix是Unix一个发行版的分支，Linux内核就来自这个系统，并且可以适用x86的个人计算机。

###  VMware WorkStation

#### 虚拟机网络模式

1. 桥接模式：虚拟地址可以和外部系统通讯，但是容易造成IP冲突。
2. NAT模式：网络地址转换模式，虚拟系统可以和外部系统通讯（通过宿主机IP），不造成IP冲突。
3. 主机模式：独立系统，不和外部产生联系。

#### 虚拟机克隆

1. 可以直接克隆虚拟机文件夹，使用VMware打开即可。
2. 也可以直接使用VMware软件中的虚拟机克隆，克隆时需要先关闭虚拟机。

#### 虚拟机快照

保存虚拟机的快照，可以在虚拟机异常时恢复到快照状态。

可以设置VMware tools安装和共享文件夹方便使用。

#### WSL卸载

wsl --list

wsl --unregister 名字

wsl --list

#### WSL自定义安装

1. 下载 Ubuntu-22.04 LTS 镜像文件
2. 创建安装目录 e:\wsl\ubuntu_v2204
3. wsl --import <名称> <解压位置> <镜像文件>`wsl --import Ubuntu-22.04 e:\wsl\ubuntu_v2204 e:\wsl\ubuntu-22.04-server-cloudimg-amd64-wsl.rootfs.tar.gz`
4. 启动`wsl -d Ubuntu-22.04 -u root` 。

### Linux

#### linux目录结构

linux的文件系统是采用层级式的树状目录结构，在此结构中最上层是根目录"/"，然后在此目录下再创建其他目录。“在Linux世界里，一切皆文件！”

根目录下有如下目录：

* /bin：存放着最常用的命令
* /sbin：SuperUser，也就是系统管理员尝试用的系统管理程序
* /home：存放普通用户的主目录，在Linux中每个用户都有自己一个目录，一般是以该用户账号名字命名
* /root：系统管理员目录，超级权限者的用户主目录
* /lib：系统开机所需要的最基本的动态链接共享库，其作用类似于windows下的DLL文件。几乎所有应用程序都需要使用这些共享库。
* /lost+found：这个目录一般是空的，当系统非法关机后，这里就存放了一些文件，此目录在图形界面是隐藏的。
* /etc：所有系统管理和应用程序的配置文件和子目录
* /usr：存放用户的应用程序和文件，类似于windows下的program files目录
* /boot：启动linux时使用的一些核心文件，包括一些链接文件和镜像文件
* /proc：是一个虚拟的目录，是系统内存的映射，访问这个目录来获取系统信息
* /srv：是service的缩写，用来存放一些服务启动之后需要提取的数据
* /sys：lunux2.6内核的一个很大的变化，该目录安装了2.6内核中新出现的一个文件系统sysfs
* /tmp：存放临时文件
* /dev：类似于windows下的设备管理器，把所有的硬件用文件方式存储
* /midea：linux系统会自动识别一些设备，例如U盘、光驱等，linux会把识别的设备挂载到这个目录下
* /mnt：提供该目录让用户临时挂在别的文件系统，可以将外部存储挂载到/mnt/上，就可以在该目录下查看内容了
* /opt：给主机额外安装软件所存放的目录，默认为空
* /usr/local：这是另一个给主机额外安装软件所安装的目录。一般是通过编译源码安装的程序。
* /var：存放着不断扩充着的东西，习惯将经常被修改的目录放在这个目录下，包括各种日志文件
* /selinux[security-enhanced linux]：是一种安全子系统，它能控制程序只能访问特定文件，有三种工作模式，可以自行设置

## Linux实操篇

### 工具

#### 使用Xshell和Xftp远程登陆Linux和文件互传

#### vi和vim文本编辑器

Linux内置vi文本编辑器，而vim是vi的增强版本。三种模式：

* 一般模式：默认进入时的模式，可以使用上下左右移动光标，可以使用删除整行或者删除字符，也可以使用复制粘贴。
* 插入模式：按下I、O、A、R或i、o、a、r可以从一般模式进入编辑模式，一般使用`i`即可。使用`esc`可以返回到一般模式。
* 命令行模式：在一般模式下输入`:`或者`/`进入命令行模式，提供相关指令，完成读取、存盘、替换、离开vim、显示行号等操作。使用`esc`可以返回到一般模式。其中命令有`:wq`、`:q`、`:q!`，分别代表保存退出、退出、强制退出并且不保存。

一些一般模式下的操作：

* `yy`：拷贝当前行，`5yy`表示拷贝当前行向下的5行
* `p`：粘贴
* `dd`：删除当前行，`5dd`表示删除当前行向下的5行
* `/查找的字符串`：可以在命令行实现查找，使用`n`找到下一个。
* `:set nu`和`:set nonu`：设置文件行号和取消文件行号
* `G`和`gg`：分别代表定位到尾行和首行
* `u`：撤销动作
* `20 shift+g`：定位到第20行

### 开关机和登录

#### 开机&重启

不管是重启系统还是关闭系统，首先要运行`sync`，把内存中的数据写入磁盘。目前的系统中`halt`、`reboot`、`shutdown`等命令均已经内置了提前的`sync`。

| 指令                                         | 含义                                        |
| -------------------------------------------- | ------------------------------------------- |
| `halt`                                       | 立即关机                                    |
| `reboot`                                     | 立即重启                                    |
| `sync`                                       | 把内存的数据同步到磁盘                      |
| `shutdown -h now`                            | 立刻进行关机                                |
| `shutdown -h 1 "hello，1分钟之后将会关机。"` | 1分钟之后关机并立刻向所有用户发送后面的信息 |
| `shutdown -r now`                            | 立刻进行重启                                |

#### 用户登录&注销

普通用户登陆后，可以使用`su - 用户名`切换登录用户。终端内输入`logout`即可注销当前用户，但是在图形运行级别无效，在运行级别3下有效。

如果进行了用户的切换，那么使用logout将会回到切换到此用户的上一个用户的登陆状态，除非是初始登录用户才会执行注销。

### 用户管理

> Linux是一个多用户多任务操作系统，任何一个要使用系统资源的用户，必须向系统管理员申请一个账号，并以这个账号身份进入系统。

#### 添加用户&指定密码

root用户可以使用`useradd 用户名`添加一个用户，会自动创建和该用户同名的home目录。也可以使用`useradd -d 指定目录 用户名`给新创建的用户指定home目录。

使用`passwd 用户名`给用户名指定密码或者修改密码。

#### 用户删除

root用户可以使用命令`userdel 用户名`删除用户。这里有两种情况，一种情况是保留用户的home目录，另一种情况是`userdel -r 用户名  `删除用户的home目录。一般情况下，建议保留被删除用户的home目录。

#### 查询用户&切换用户

查询用户的语法是`id 用户名`。查看当前登录用户使用指令`whoami`或者`who am I`，这个指令查询的是这一次最初登录时使用的用户，而不是后续使用su切换的用户。

当当前用户的权限不够时，可以使用`su - 用户名`指令切换到高权限用户，比如root用户。其中，从权限高的用户切换到权限低的用户，不需要输入密码，反之需要。当需要返回到原来用户时，可以使用exit/logout指令。

#### 用户组

组类似于角色，系统可以对有共性（权限）的多个用户进行统一的管理。

使用`groupadd 组名`新增组，使用`groupdel 组名`删除组。可以选择在新增用户时使用`-g`参数直接为其指定组，对应指令为`useradd -g 组名 用户名`。如果在新建用户时没有指定组，会创建与用户同名的组，并将此用户加入该组。使用指令`usermod -g 用户组 用户`可以修改用户的组，如果指定的组不存在则创建。

#### 用户和组相关文件

* /etc/passwd文件：用户的配置文件，记录用户的各种信息。

  实例：`szl:x:1000:1000:szl:/home/szl:/bin/bash`

  含义：`用户名:口令:用户标识号:组标识号:注释性描述:主目录:登录shell`

* /etc/shadow文件：口令的配置文件

  实例：`szl:$6$f6MBrHNaG/C6Uwr4$BHbJ604YhOhlDcfjk.C.TKRg...::0:99999:7:::`

  含义：`登录名:加密口令:最后一次修改时间:最小时间间隔:最大时间间隔:警告时间:不活动时间:失效时间:标志`

* /etc/group文件：组的配置文件，记录linux包含的组的信息

  实例：`szl:x:1000:szl`

  含义：`组名:口令:组标识号:组内用户列表`

### Linux指令

#### 指定运行级别runlevel

运行级别分为以下6种

0：关机

1：单用户（可以用来找回丢失密码）

2：多用户状态没有网络服务（基本没用）

3：多用户状态有网络服务（最常用）

4：系统未使用保留给用户（不用）

5：图形界面

6：重启

常用运行级别是3和5，也可以切换运行级别，使用`init 运行级别`命令来完成。也可以指定默认的运行级别，在CentOS7之前，运行级别需要在/etc/inittab文件中更改，在后续做了简化：使用multi-user.target表示级别3，graphical.target表示级别5。

可以使用`systemctl get-default`来查看系统当前的运行级别，使用`systemctl set-default TARGET.target`来设置默认运行级别。

> 面试题：如何找回root密码？
>
> 1. 在启动界面按e进入编辑模式
> 2. 在编辑界面中使用键盘上下键把光标移动到以"Linux16"开头的行，在行的最后面输入init=/bin/sh
> 3. 输入完成后，按快捷键Ctrl+X进入单用户模式
> 4. 接着，输入mount -o remount,rw /
> 5. 在新的一行输入passwd回车，输入密码并确认密码即可
> 6. 然后输入touch /.autorelabel，回车
> 7. 再输入exec/sbin/init，回车之后系统将自动重启，新的密码就会生效

#### Linux下的帮助指令

可以使用man来获得帮助信息，使用方式是`man [命令或配置文件]`，如`man ls`。

可以使用help来获得shell内置命令的帮助信息，指令为`help 命令`，如`help cd`。

#### 文件目录类指令

* pwd：显示当前工作目录的绝对路径

* ls：可选参数有`-a`和`-l`

* cd：使用`cd ~`或者`cd :`回到自己的家目录，使用`cd ..`回到当前目录的上一级目录

* mkdir：创建目录，参数`-p`可以创建多级目录

* rmdir：删除空目录，使用`rm -rf`删除非空目录

* touch：创建一个空文件

* cp：使用`cp 选项 source dest`指令将source拷贝到dest目录下，可选参数`-r`代表递归复制整个文件夹。使用`\cp`代替`cp`可以在拷贝时强制执行进行覆盖而不进行提示。

* rm：移除文件或者目录，可选参数有`-r`（递归删除整个文件夹）、`-f`（强制删除不提示）

* mv：移动文件与目录或者重命名。使用指令`mv oldName newName`和`mv source dest/`分别进行文件重命名和移动。还可以使用`mv source dest/newName`进行移动并且重命名。目录同理。

* cat：查看文件，使用`-n`选项可以显示行号。为了浏览方便可以带上管道命令`| more`，使用enter查看下一行，使用space翻页。

* more：是一个基于VI编辑器的文本过滤器，它以全屏幕的方式按页显示文本文件内容。more内置了若干交互快捷键

  | 操作   | 功能说明               |
  | ------ | ---------------------- |
  | space  | 向下翻一页             |
  | enter  | 向下翻一行             |
  | q      | 立即离开               |
  | ctrl+F | 向下滚动一屏           |
  | ctrl+B | 返回上一屏             |
  | =      | 输出当前行行号         |
  | :f     | 输出文件名和当前行行号 |

* less：用来分屏查看文件内容，它的功能与more指令类似，但是比more指令更加强大，支持各种显示终端。less指令在显示文件内容时，并不是一次将整个文件加载之后才显示，而是根据显示需要加载内容，对于现实大型文件具有较高的效率。

  | 操作     | 功能说明                           |
  | -------- | ---------------------------------- |
  | space    | 向下翻一页                         |
  | pagedown | 向下翻一页                         |
  | pageup   | 向上翻一页                         |
  | /字串    | 向下查找字串，n向下查找，N向上查找 |
  | ?字串    | 向上查找字串，n向上查找，N向下查找 |
  | q        | 立即离开                           |

* echo：输出内容到控制台，例如`echo $PATh`或者`echo $HOSTNAME`或者`echo "hello world!"`，可以在末尾追加`> 文件`表示将内容重定向覆盖到文件中。

* head：显示文件开头部分内容，默认是显示10行，可以使用`-n`指定显示行数，如`head -n 5 文件`

* tail：显示文件结尾部分内容，默认是显示10行，可以使用`-n`指定显示行数，如`tail -n 5 文件`。tail可以使用`-f`实时追踪文件变化，如`tail -f 文件`，退出监控使用ctrl+d                     。

* `>`和`>>`：分别表示输出重定向和追加，可以跟在ls、cat、echo等指令后，其中>表示覆盖，>>表示追加。

* ln：软链接，也称为符号链接，类似于windows下的快捷方式，主要存放连接其他文件的路径，基本语法是`ln -s 源文件或者目录 软链接名`，如果想要删除直接`rm 软链接名`即可。

* history：查看已经执行的历史命令，如果想要查看10条，可以指定`history 10`，查看之后使用`!20`执行历史指令中的第20条指令。

#### 时间日期类指令

date指令可以用来显示当前时间，默认显示效果为`2023年 04月 13日 星期四 14:55:05 CST`，可以在date后指定显示格式，其中%Y、%m、%d、%H、%M、%S分别表示年、月、日、小时、分钟、秒。例如`date "+%Y-%m-%d  %H:%M:%S"`将会打印出`2023-04-13  14:58:03`。

还可以使用`-s`选项设置系统当前时间，例如`date -s "2020-11-03 20:02:10"`

cal指令可以显示本月日历，显示某一年的日历只需要在后方指定年份。

#### 查找指令

find指令将从指定目录向下递归的遍历其各个子目录，将满足条件的文件或目录显示在终端。语法为`find [搜索范围] [选项]`，其中选项可以使用正则化匹配或者下面的选项。

* -name <查询方式>，按照指定的文件名查找模式查找文件，例如`find /home hello.txt`
* -user <用户名>，查找指定用户名所有的文件，例如`find /opt -user szl`
* -size <文件大小>，按照指定的文件大小查找文件，+200M代表大于，-200M代表小于，200M代表等于。例如`find / -size -200M`，其中文件大小单位有k、M、G
* `ls -lh`可以按照hunman能看懂的方式以列表形式显示文件，其中文件大小不再是字节。

locate指定可以快速定位文件路径。它是利用了建立好的locate数据库实现快速定位，这个数据库包含了系统中所有文件名及其路径，所以locate无需遍历整个文件系统，查询速度很快。但是由于locate指令基于数据库进行查询，所以第一次运行前，必须使用updatedb更新数据库。使用方式为`locate hello.txt`

which指令可以查看某个指令在哪个目录下，如`which python`或`which ls`

grep指令是过滤查找，其基本语法为`grep [选项] 查找内容 源文件`，`-n`选项显示匹配行和行号，`-i`忽略字母大小写。

管道符号`|`，表示将前一个命令的处理结果输出传递给后面的命令处理。所以我们这里有两种方式实现查找hello.txt中的yes字符串。

```shell
[root@centos7 ~]# grep -n "public" hello.java 
1:public class Hello {
3:	public static void main(String[] args){
[root@centos7 ~]# cat hello.java | grep -n "public"
1:public class Hello {
3:	public static void main(String[] args){
```

#### 压缩和解压指令

使用gzip将文件压缩为.zip格式，使用gunzip对文件进行解压，直接使用`gzip 文件`或者`gunzip 文件.zip`即可。

zip用于压缩目录或者文件，unzip进行解压，常用于项目的打包发布。使用方式为`zip [options] XXX.zip 需要压缩的内容`和`unzip [options] XXX.zip`。zip常用选项是`-r`，也就是递归压缩，即压缩目录。unzip的常用选项是`-d <目录>`用于指定解压后文件的存放位置。

tar指令用于打包和解压文件（备份文件），最后打包后的文件是.tar.gz为后缀的文件。基本语法是`tar [options] XXX.tar.gz 打包的内容`，选项有如下几种

* -c：等同于--create，建立新的备份文件。
* -v：等同于或--verbose，显示指令执行过程。
* -f <备份文件>：等同于--file=<备份文件> ，指定备份文件
* -z：等同于--gzip或--ungzip，通过gzip指令处理备份文件。
* -x：从备份文件中还原文件。

一般使用`-zcvf`打包并压缩文件，使用`-zxvf`解包并解压文件。如`tar -zcvf animal.tar.gz pig.txt cat.txt`。

解包并解压文件到当前目录指令为：`tar -zxvf animal.tar.gz`

解压到选中的目录下指令为：`tar -zxvf animal.tar.gz -C 目录`

### 组管理和权限管理

> Linux组基本介绍
>
> 在linux中，每个用户必须属于一个组，不能独立于组外。在Linux中每个文件都有对应的所有者、所在组、其他组的概念。

#### 文件所有者

一般情况下文件的所有者为文件的创建者，谁创建了该文件，自然就是该文件的所有者。可以使用指令`ls -ahl`查看文件的所有者。使用`chown 用户名 文件名`来更改文件的所有者。

#### 文件/目录所在组

某用户创建文件/目录后，该文件所在组就是该用户所在的组。可以使用`chgrp 组名 文件名`改变文件所在的组。注意文件所在组和文件所有者所在组不一定非要一致。

#### 用户所在组

添加用户时，可以使用-g或者-d指定将该用户添加到哪个组和指定home目录。同样的，也可以使用`usermod -g 新组名 用户名`和`usermod -d 目录名 用户名`做相应修改。

#### 权限基本介绍

`ls -l`中显示的一行内容如下：

`-rw-r--r--. 1 root root  110 4月  12 22:14 hello.java`

* 第1列有10位，其0-9位含义如下：

  * 0：确定文件类型
    * l：链接
    * d：目录
    * c：字符设备文件，例如鼠标和键盘
    * b：块设备，如硬盘
    * -：普通文件

  * 1-3：确定该文件所有者拥有该文件的权限--User

  * 4-6：确定该文件所属组拥有该文件的权限--Group

  * 7-9：确定其他用户拥有该文件的权限--Other

* 第2列是一个数字，表示目录中的文件数+子目录数
* 第3列代表所属用户
* 第4列代表所在组
* 第5列表示文件大小，单位为字节，如果是目录显示为固定的4096字节
* 第6列代表最后修改日期
* 第7列表示文件名

#### rwx权限

rwx作用到文件时：

* r：代表可读
* w：代表可写，但不代表可以删除该文件，只用对文件所在目录具有可写权限才能进行对文件的删除。
* x：可执行

rwx作用到目录时：

* r：可读，可以使用ls查看
* w：可修改，对目录内文件创建、删除和对目录重命名
* x：可执行，也就是可以使用cd进入目录

注意在Linux中，rwx可用数字表示，r=4、w=2、x=1，因此rwx=7

#### 权限修改

使用chmod指令修改文件或者目录的权限，chmod有两种使用方式。

可以通过+ - =的方式修改权限。其中u代表所属人、g代表所在组、o代表其他人、a代表所有人。

* `chmod u=rwx,g=rx,o=x 文件目录名`
* `chmod o+w,g+x 文件目录名`
* `chmod a-x 文件目录名`

使用数字方式，比如`chmod 751 文件或目录名`代表分别给u、g、o赋予权限rwx、rx、x

#### 修改文件所有者和所在组

使用`chown newoner 文件/目录`改变文件/目录的所有者。或者使用`chown newoner:newgroup 文件/目录`同时更改所有者和所在组。如果是目录，需要加入-R使命令对其下的所有子文件和子目录生效`chown -R newoner 目录`。

使用`chgrp newgroup 文件/目录`改变文件/目录所在组。同样需要加入-R使命令对其下的所有子文件和子目录生效。

### 定时任务调度

> 任务调度指系统在某个时间执行特定的应用和程序，有如下两种
>
> 1. 系统工作：有些重要的工作必须周而复始，比如病毒扫描等
> 2. 个别用户工作：个别用户可能会希望执行某些程序，比如对mysql数据库的备份等

#### crond任务调度

使用crontab进行定时任务的设置，基本语法是crontab [options]，常用的选项有

* -e：新增/编辑crontab定时任务
* -l：查询crontab定时任务
* -r：删除当前用户所有crontab定时任务

重启任务调度指令为service crond restart

例如定时任务`*/1 * * * * ls -l /etc/ > /tmp/to.txt`，五个占位符分别表示分钟、小时、日、月、星期。在这里这个定时任务就是每一分钟就把/etc/目录的ls -l指令打印内容覆盖到文件中去。占位符可以使用的特殊符号有

* `*`：任何时间
* `，`：代表不连续的时间
* `-`：代表连续的时间
* `*/n`：代表每隔多久执行一次

如`*/2 3-4 1,15 * 1`代表每月是周1的1号和15号的3点到4点的每2分钟执行一次.

在crontab后可以指定.sh脚本文件运行多条指令。

#### at定时任务

at命令是一次性定时计划任务，at的守护进程atd会以后台模式运行，并在默认情况下每60s检查一次作业队列。有作业时，会检查作业运行时间，与当前时间匹配的话就执行任务并出队列。使用at命令时，要保证atd进程在运行。atd进程运行状态使用指令`ps -ef | grep atd`查看。

at命令格式形如`at [option] [time]` ，并使用Ctrl+D结束at命令的输入。其中可选项为：

* -m：指定的任务完成后，将给用户发送邮件，即使没有标准输出
* -I：atq的别名，查询还未执行的工作任务
* -d：atrm的别名，删除特定编号的任务
* -v：显示任务将被执行的时间
* -c：打印任务内容到标准输出
* -V：显示版本信息
* -q < queue>：使用指定的队列
* -f <file>：从指定文件读入而不是从标准输入读入
* -t <time>：以时间参数形式提交要运行的任务

at指定时间的方法：

* 接受在当天的hh:mm的时间指定，如果时间已经过去，则第二天这个时间执行
* midnight、noon、teatime
* 可以采用12小时制，9AM或12PM
* 指定具体日期month day或mm/dd/yy或dd .mm.yy，指定的日期跟在指定的时间后面
* 相对计时法，now+count 时间单位，单位有minutes、hours、days、weeks等
* today、tomorrow

例如`at 5pm + 2 days`、`at 5pm torrow`、`at now + 2 minutes`等

### Linux磁盘

#### Linux分区

Linux只有一个根目录，一个独立且唯一的文件结构，Linux中每个分区都是用来组成整个文件系统的一部分。linux采用挂载的处理方法将一个分区和一个目录联系起来，这时将载入的一个分区将使它的存储空间在一个目录下获得。

linux硬盘分为IDE硬盘和SCSI硬盘，目前基本上都是SCSI硬盘。对于IDE硬盘，驱动器标识符为"hdx\~"，其中hd表明分区所在设备的类型，也就是IDE；x表示盘号，也就是第几块硬盘，一般使用abcd表示；\~代表分区，前四个分区用数字1-4表示，他们是主分区或扩展分区，从5开始就是逻辑分区。对于SCSI硬盘驱动器标识符为"sdx\~"，其余表示方式和IDE一样。

使用lsblk或者lsblk -f查看所有设备挂载情况和详细信息。

#### Linux新增硬盘

1. 虚拟机新增硬盘/实体机新增硬盘，重启之后使用`lsblk`可以查看到新的硬盘sdb
2. 对硬盘sdb进行分区，使用命令`fdisk /dev/sdb`进行分区
   1. m显示命令列表
   2. p显示磁盘分区，同fdisk -l
   3. n新增分区
   4. d删除分区
   5. 写入并退出
3. 对分区格式化，命令是`mkfs -t ext4 /dev/sdb1`
4. 挂载，使用`mount /dev/sdb1 挂载目录(/newdisk/)`将分区挂载到目录，也可以使用`umount /dev/sdb1`或者`umount /newdisk`将分区从目录卸载。注意这种使用命令行挂载的方式再重启之后会失效。

可以通过修改/etc/fstab文件实现永久挂载，添加完成后，执行`mount -a`即刻生效。

#### 磁盘情况查询

使用df -h命令查询整体磁盘使用情况。查询指定目录的磁盘占用情况使用命令`du -h 目录`，如果不指定目录默认查询当前目录。其他options如下：

* -s：该目录汇总值
* -h：带计量单位，humman
* -a：含文件
* --max-depth=1：子目录深度
* -c：列出明细的同时，增加汇总值

#### 磁盘文件统计指令

1. 统计/opt目录下文件的个数`ls -l /opt | grep "^-" | wc -l`
2. 统计/opt目录下目录的个数`ls -d /opt | grep "^-" | wc -l`
3. 统计/opt目录下文件的个数，包括子文件夹`ls -lR /opt | grep "^-" | wc -l`
4. 统计/opt目录下目录的个数，包括子文件夹`ls -dR /opt | grep "^-" | wc -l`
5. 树状显示目录`tree /home`

### Linux网络配置

ifconfig查看Linux网络连接情况，使用ping命令测试连通性。

#### 配置固定IP

第一种方式是设置DHCP自动分配ip地址。

第二种方法则是手动指定ip地址。直接通过修改配置文件来指定ip，并且可以连接到外网。对应配置文件是`vim /etc/sysconfig/network-scripts/ifcfg-ens33`。将BOOTPROTO从dhcp修改为static，加入`IPADDR=192.168.200.130`和`GATEWAY=192.168.200.2`和`DNS1=192.168.200.2`。同时对于虚拟机也要修改网关，在VMware软件中修改NAT模式下的子网和网关ip地址。最后一步重启网络`service network restart`或者重启系统`reboot`即可。

#### 主机名和hosts映射

查看主机名直接输入hostname，修改主机名需要修改/etc/hostname文件，重启后生效。

设置host映射，windows和linux是不同的。在windows下，需要修改C:\Windows\System32\drivers\etc\hosts文件，在其中加入linux主机的ip和主机名，如`192.168.200.130 centos7.6`；而在linux下，需要修改文件/etc/hosts，加入windows主机的ip和主机名，如`192.168.200.1 s2drag0n`。设置映射之后就可以直接ping主机名即可。

域名解析机制：首先去**浏览器缓存**查找，没有则去本地DNS解析缓存查找，再没有就到**hosts文件**中查找，最后才会去**域名服务器DNS**进行解析。

在windows下可以查看DNS域名解析缓存，使用`ipconfig /displaydns`命令；也可以手动清理dns缓存，使用`ipconfig /flushdns`命令。

### 进程管理

在linux中，每个执行的程序都被称为一个进程，每个进程都分配一个ID号（pid，进程号）。每个进程都可能以两种方式存存在，即前台与后台。前台进程就是用户目前的屏幕上可以进行操作的进程，而后台进程则是屏幕上无法看到但是却是在以后台方式执行的进程。一般系统的服务都是以后台进程的方式存在的，而且都会常驻在系统中，直到关机才结束。

#### ps指令

ps指令是用于查看目前系统中有哪些进程正在执行，并查看他们的执行状况。options有-a显示当前终端所有进程信息、-u以用户的格式显示进程信息、-x显示后台进程运行的参数。options可以组合使用，且可以加上管道过滤grep。`ps -ef`和`ps -aux`分别是System Ｖ风格和BSD 风格，`ps -aux`最初用到Unix Style中，而`ps -ef`被用在System V Style中，两者输出略有不同。现在的大部分Linux系统都是可以同时使用这两种方式的。-e代表显示所有进程，-f表示全格式，包括父进程pid。

#### 终止进程

使用`kill [options] 进程号`可以通过指定进程号来杀死进程，options的常用选项为-9，表示强迫进程立即停止。或者使用`killall 进程名称`杀死此进程及其所有子进程，支持[通配符](https://baike.baidu.com/item/%E9%80%9A%E9%85%8D%E7%AC%A6/92991)。

实现踢某用户下线：

1. 使用`ps -aux | grep sshd`查找该用户使用的登陆进程
2. kill相应的pid

终止远程服务sshd，在适当时候重启：

1. 使用`ps -aux | grep sshd`查询/usr/sbin/sshd进程
2. kill相应pid
3. 重启：systemctl start sshd.service

终止多个gedit（linux图形界面文本编辑器）：使用`killall gedit`。

强制杀死一个终端：

1. `ps -aux | grep bash`查找终端进程
2. 需要使用`kill -9 pid`杀死目标终端，可以杀死自己。

#### 查看进程树

`pstree [options]`可以更加直观的查看进程信息，常用选项有-p显示进程的pid；-u显示进程的所属用户。

### 服务管理

服务service本质上就是进程，但是是运行在后台的，通常都会监听某个端口，等待其他程序的请求，因此又称为守护进程。服务=守护进程=后台进程

#### service管理指令

1. `service 服务名 [start | stop | restart | reload | status]`
2. 在CentOS7以后，很多服务不再使用service，而是使用systemctl
3. service指令仍可以管理的服务可以在/etc/init.d/目录下查看

```shell
[root@centos7 ~]# ls -al /etc/init.d/
总用量 92
drwxr-xr-x.  2 root root  4096 4月  12 19:27 .
drwxr-xr-x. 10 root root  4096 4月  12 17:52 ..
-rw-r--r--.  1 root root 18281 8月  24 2018 functions
-rwxr-xr-x.  1 root root  4569 8月  24 2018 netconsole
-rwxr-xr-x.  1 root root  7923 8月  24 2018 network
-rw-r--r--.  1 root root  1160 10月 31 2018 README
-rwxr-xr-x.  1 root root 44969 4月  12 19:27 vmware-tools
```

使用setup可以看到所有服务，以及该服务是否会开机自启和是否贵service指令管理

#### 服务运行级别

运行级别上文有提到。

Linux开机的流程是

1. 开机
2. BIOS
3. /boot
4. systemd进程1
5. 运行级别
6. 运行级别对应的服务

#### chkconfig指令指定服务对应的运行级别

这是一个传统的指令，只能管理/etc/init.d/下的服务。

* 查看chkconfig管理的所有服务在各个运行级别下的开关状态：`chkconfig --list`
* `chkconfig 服务名 --list`
* `chkconfig --level 5 服务名 on/off`

使用chkcongif重新设置服务后需要系统reboot后才能生效。

#### systemctl管理指令

使用语法为`service [start | stop | restart | reload | status] 服务名 `。

systemctl指令管理的服务可以在/usr/lib/systemd/system/目录下查看。

```shell
[root@centos7 ~]# ls -l /usr/lib/systemd/system/ | grep fire
-rw-r--r--. 1 root root  657 10月 31 2018 firewalld.service
[root@centos7 ~]# 
```

可以使用systemctl查看和设置服务的自启动状态（注意在CentOS7以后，运行级别简化为3和5，所以这里默认是在3和5状态下的自启动状态）。

* `systemctl list-unit-files`查看服务的开机自启状态
* `systemctl enable 服务名`设置服务开机自启
* `systemctl disable 服务名`关闭服务开机自启
* `systemctl is-enabled 服务名`查看服务开机自启状态

#### 打开或关闭指定端口firewall

使用firewall指令

* 打开端口：firewall-cmd --permanent --add-port=端口号/协议
* 关闭端口：firewall-cmd --permanent --remove-port=端口号/协议
* 必须要重新载入，上述设置才能生效：firewall-cmd --reload
* 查询端口是否开放：firewall-cmd --query-port=端口号/协议

查询侦听特定端口号服务采用的协议方式为`netstat -anp | more`.

#### 动态监控top

top和ps指令很相似，但是不同ps的是，top在执行一段时间时间内可以更新正在运行的进程。选项有

* -d 秒数：指定top命令每隔几秒更新一次，默认是3秒
* -i：使top不显示任何闲置或者僵死进程(死掉了但是占用内存的进程)
* -p：通过指定监控进程PID来仅仅监控某个进程的状态

交互操作有

* P：按cpu使用率排序
* M：按内存占用排序
* N：按照pid排序
* q：退出
* 输入u，回车，再输入用户名：查看某用户的进程
* 输入k，回车，输入进程pid，可以杀死该进程

#### 监控网络状态netstat

可选项有：

* -an：按一定顺序排列输出
* -p：显示哪个进程在调用

检测主机连接命令ping，Ping命令使用的是ICMP协议，不是端口号。ICMP是控制协议，不需要端口号。不走传输层，所以不需要端口号。

### rpm包管理

rpm用于互联网下载包的打包及安装，它包含在某些Linux分发版（suse，redhat，centos等）中。它生成具有.RPM扩展名的文件，RPM是Redhat Package Manager的缩写，类似于windows的setup.exe。

#### 查询rpm包

查询已安装的rpm列表：`rpm -qa | grep firefox`，结果会返回`firefox-68.2.0-2.el8_0.x86_64`，这代表了：

* 名称：firefox
* 版本号：68.2.0-2
* 适用操作系统：el8_0.x86_64
* 如果是i686、i386表示32位系统，noarch表示通用

其他查询选项

* 也可以直接`rpm -qa firefox`来查询指定包是否安装。
* `rpm -qi firefox`查询软件包的具体信息。
* `rpm -ql firefox`查询软件包中的文件及其路径。
* `rpm -qf 文件全路径名`查询文件所属的软件包。

#### 卸载rpm包

`rpm -e PRM包名称 //earse`

细节：如果其他软件包依赖于你要写在的软件包，则会产生错误信息，增加参数`--nodeps`就可以强制删除。

#### 安装rpm包

`rpm -ivh RPM包全路径名称`

参数说明：

* i=install
* v=verbose 提示
* h=hash 进度条

#### yum

yum是一个Shell前端软件包管理器，基于rpm包管理，可以从指定的服务器自动下载rpm包并进行安装，并自动处理依赖关系，一次安装所有依赖的软件包。

基本指令：

* 查询yum服务器是否有需要的软件`yum list | grep 软件名`
* 安装指定的yum包`yum install xxx`

### Shell编程

shell是一个命令行解释器，它为用户提供了一个向Linux内核发送请求以便运行程序的界面系统级程序，用户可以用shell来启动、挂起、停止甚至编写一些程序。命令行指令包括shell脚本都需要经过shell解释才能被linux内核看懂。

#### shell脚本执行方式

脚本格式要求：

* 以`#!/bin/bash`开头
* 需要有可执行权限
*  脚本名约定以`.sh`结尾

常用执行方式：

* 首先赋予脚本可执行权限+x，再执行脚本（`./脚本名`）
* 不用赋予权限+x，直接执行（`sh 脚本名`）

#### shell变量

Linux中shell变量分为系统变量和用户自定义变量

* 系统变量：\$HOME、\$PWD、\$SHELL、\$USER等
* 显示当前shell中所有变量set

自定义变量

* 定义变量：`变量名=值`
* 撤销变量：`unset 变量`
* 声明静态变量：`readonly 变量=值`，且不能被unset
* 输出变量：`echo $变量名`
* `echo 变量名=\$变量名`等价于`echo "变量名=\$变量名"`
* 等号两侧不能有空格
* 变量名称一般习惯大写

将命令的返回值赋给变量

* A=\`date\`反引号，运行里面的命令，并把结果返回给变量A
* A=\$(date)和上面的方式等价

#### 设置环境变量

linux环境变量配置文件为/etc/profile，在此文件中

* `export 变量名=值`可以将shell变量输出为环境变量/全局变量
* `source 配置文件`让修改后的配置文件立即生效

shell脚本的单行注释为`#`，多行注释为`:<<!换行 内容 换行 !`

#### 位置参数变量

当我们执行脚本时，如果希望shell脚本获取到命令行赋予的参数信息，就可以使用位置参数变量，如`./myshell.sh 100 200`，这就是一个执行shell的命令行，可以在shell脚本中获取到参数信息。基本语法为

* \$n：其中n为数字，\$0代表命令本身，\$1-\$9代表第1个到第9个参数，第10个参数需要使用\${10}来指定
* \$*：代表命令行中所有参数，并将其视为整体
* \$@：代表命令行中所有参数，并将每个参数区分对待
* \$#：代表命令行中所有参数的个数

#### 预定义变量

shell设计者事先定义好的变量，可以在shell脚本中直接使用

* \$\$：当前进程的进程号pid
* \$!：后台运行的最后一个进程的进程号
* \$?：最后一次执行的命令的返回状态，如果这个变量的值为0，证明上一个命令执行正确，如果这个变量的值非0，则证明执行不正确。

#### 运算符

基本语法

* `$((运算式))`或`$[运算式]`或者`expr m + n`
* 注意expr运算符间必须有空格，如果希望将整个expr的结果赋给某个变量，使用反引号\`\`
* 注意expr的乘法需要转义\\*
* /、%则直接使用

#### 条件判断

[ condition ]非空返回true，可以使用\$?验证最后一次执行的命令返回状态（0为true，1为false），注意condition前后都有空格。

`[ condition ] && echo OK || echo notok`

常用判断语句

* =用于字符串比较
* 整数比较
  * -lt小于
  * -le小于等于
  * -eq等于
  * -gt大于
  * -ge大于等于
  * -ne不等于
* 按照文件权限判断
  * -r有读的权限
  * -w有写的权限
  * -x有执行的权限
* 按照文件类型判断
  * -f文件存在且是一个常规文件
  * -e文件存在
  * -d文件存在且是一个文件夹

#### if条件判断

```shell
#!/bin/bash
if [ "ok" = "ok" ]
then
	echo "equal"
fi

# if [ 23 -ge 22 ]
# if [ -f /root/aaa.txt ]
# if也有相应的elif表示else if
if [ option1 ]
then
	# program1
elif [ option2 ]
then 
	# program2
fi
```

#### case语句

基本语法如下

```shell
case $var in
"val1")
# program1
;;
"val2")
# program2
;;
# ......
*)
# programDefault
;;
esac
```

#### for和while循环

for基本语法一

```shell
for var in val1 val2 val3......
do
# program
done

# 此程序可以测试$*和$@的区别
```

for基本语法二

```shell
for ((初始值;循环控制条件;变量变化++--))
do
# program
done
```

while基本语法

```shell
while [ 条件判断式 ]
do
# program
done
```

#### read读取控制台输入

`read [options] 变量`

* -p：指定读取值时的操作符
* -t：指定读取值时等待的时间（秒）

```shell
read -p "请输入一个数NUM1=" NUM1
read -t 10 -p "请在十秒内输入一个数NUM2=" NUM2
```

#### 函数

shell变成有系统函数和自定义函数

##### 系统函数basename

* 功能：返回完整路径最后/的部分，常用于获取文件名
* `basename [pathname] [suffix]`
* `basename [str] [suffix]`
* basename删去所有的前缀包括最后一个/字符，然后显示字符串
* 如果指定了suffix为后缀，basename会将pathname或者string中的suffix去掉、

```shell
basename /root/aaa.txt
# 结果会打印aaa.txt
```

##### 系统函数dirname

功能：返回完整路径最后一个/前面的部分，常用于返回路径部分

##### 自定义函数

```shell
function funname(参数列表)
{
	Action;
	[return int;]
}
# 调用方式为
funname 参数列表
```

#### 综合案例--数据库备份

要求：

* 每天凌晨2：30备份数据库hspedu到/data/back/db
* 备份开始和备份结束能够给出相应的提示信息
* 备份后的文件要求以备份时间为文件名，并打包成.tar.gz的形式
* 在备份的同时，检查如果有10天前备份的数据库文件，如果有就将其删除

```shell
#!/bin/bash
# 备份目录
BACKUP=/data/back/up
# 当前时间
DATETIME=$(date + %Y-%m-%d_%H%M%S)
echo $DATETIME
# 数据库的地址
HOST=localhost
# 数据库用户名
DB_USER=root
# 数据库passwd
DB_PW=xxxxxx
# 备份的数据库名
DATABASE=hspedu

# 创建备份目录，如果不存在就创建
[ ! -d "${BACKUP}/${DATATIME}" ] && mkdir -p "${BACKUP}/${DATATIME}"

# 备份数据库
mysqldump -u${DB_USER} -p${DB_PW} --host=${HOST} -q -R --databases ${DATABASE} |gzip > ${BACKUP}/${DATATIME}/${DATATIME}.sql.gz

# 将文件打包票为tar.gz
cd ${BACKUP}
tar -zcvf $DATETIME.tar.gz ${DATETIME}
# 删除对应的备份目录
rm -rf ${BACKUP}/${DATETIME}

# 删除十天前的备份文件
find ${BACKUP} -atime +10 -name "*.tar.gz" -exec rm -rf {} \;
echo "备份数据库${DATABASE}成功"

# 调用时，使用
crontab -e
# 编辑定时任务为
30 2 * * * /usr/sbin/mysql_db_back.sh
# 查看当前存在的任务调度列表
crontab -l
```

## Linux高级篇

### Python定制篇--Ubuntu

#### APT软件管理

apt（Advanced Packaging Tool）

在/etc/apt/sources.list中记录了一个美国的服务器地址，这个服务器上有很多apt软件。在国内网络环境内有很多apt的镜像网站，如果将配置中的服务器地址修改为镜像地址，就可以方便的在国内访问。

相关命令

* **sudo apt-get update 更新源**
* **sudo apt-get install package 安装包**
* **sudo apt-get remove package 删除包**
* sudo apt-cache search package 搜索软件包
* **sudo apt-cache show package 获取包的相关信息，如说明、大小、版本等**
* sudo apt-get install package --reinstall 重新安装包
* sudo apt-get -f install 修复安装
* sudo apt-get remove package --purge 删除包，包括配置文件等
* sudo apt-get build-dep package 安装相关的编译环境
* sudo apt-get upgrade 更新已安装的包
* sudo apt-get dist-upgrade 升级系统
* sudo apt-cache depends package了解使用该包依赖那些包
* sudo apt-cache rdepends package 查看该包被哪些包依赖
* **sudo apt-get source package 下载该包的源代码**

配置镜像地址

1. 在修改服务器之前先备份一下原来的配置文件

   `sudo cp /etc/apt/sources.list /etc/apt/sources.list.backup`

2. 找到[清华源](https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/)页面的配置代码放入新的配置文件即可

3. 更新源

   `sudo apt-get update`

#### SSH远程登陆

如果没有安装netstat服务，可以使用`apt install net-tools`安装。

ubuntu默认没有安装SSH服务端程序，使用netstat -an可以发现并没有监听22端口。

安装SSH服务端和客户端

`sudo apt-get install openssh-server`

启动服务

`service sshd start`

从一台linux系统远程登陆另一台linux系统

`ssh 用户名@ip`

退出使用指令

`exit`或者`logout`

### 日志管理

日志文件是重要的系统信息文件，其中记录了许多重要的系统事件，包括用户的登录信息、系统的启动信息、安全信息、邮件相关信息、各种服务相关信息等。

日志对于安全来说也很重要，它记录了系统每天发生的各种事情，通过日志来检查错误发生的原因，或者受到攻击时攻击者留下来的痕迹。总体来说，日志是用来记录重大事件的工具。

/var/log/目录就是系统日志的保存位置。

![image-20230426213345199](https://raw.githubusercontent.com/s2drag0n/Pictures/main/202304262133242.png)

#### 常用的日志

| 日志文件              | 说明                                                         |
| --------------------- | ------------------------------------------------------------ |
| **/var/log/boot.log** | 系统启动日志                                                 |
| **/var/log/cron**     | 记录与系统定时任务相关的日志                                 |
| /var/log/cups/        | 记录打印信息的日志                                           |
| /var/log/dmesg        | 记录系统在开机时内核自建的信总。可以使用dmesg命令直接查看。  |
| /var/log/btmp         | 记录错误登陆的日志。这是个二进制文件，不能直接用VI查看，需要使用lastb命令查看。 |
| **/var/log/lasllog**  | 记录系统中所有用户最后一次的登陆时间的日志。这个文件也是二进制文件，需要使用lastlog命令查看。 |
| **/var/log/mailog**   | 记录邮件信息的日志。                                         |
| **/var/log/message**  | 记录系统重要消息的日志，这个日志文件会记录linux系统中绝大多数重要信息。如果系统出现问题，首先应检查这个日志文件。 |
| **/var/log/secure**   | 记录验证和授权方面的信息，只要涉及账户和密码的程序都会记录，比如系统的登录、ssh的登录、su切换用户、sudu授权、甚至添加用户和修改用户密码也都会记录在此。 |
| /var/log/wtmp         | 永久记录所有用户的登录、注销信息，同时记录系统的启动、重启、关机事件。是二进制文件，需要使用last命令查看。 |
| **/var/log/ulmp**     | 记录当前已经登陆的用户的信息，这个文件会随着用户登录和注销而不断变化，只记录当前登陆用户的信息。这个文件不能用Vi查看，而是要使用w、who、users等命令查看。 |

#### 日志管理服务rsyslogd

日志服务的配置文件/etc/rsyslog.conf的作用就是将日志写入相应的文件

![image-20230426213423018](https://raw.githubusercontent.com/s2drag0n/Pictures/main/202304262134058.png)

CentOS6日志服务是syslogd，不过rsyslogd兼容syslogd

查询rsyslogd服务是否启动

`ps aux | grep "rsyslog" | grep -v "grep"`

查询rsyslogd服务的自启动状态

`systemctl list-unit-files | grep rsyslog`

由日志服务rsyslogd记录的日志文件，其格式包含以下4列

* 事件产生时间
* 产生事件的服务器的主机名
* 产生事件的服务名或程序名
* 时间的具体信息

#### 日志轮替

日志轮替就是把旧的日志文件移动并改名，同时建立新的空日志文件，当旧的日志文件超出保存的范围后，就会进行删除。

日志轮替规则配置目录为/etc/logrotate.d/，全局规则为/etc/logrotate.conf，也可以为某个日志文件指定自定义的规则，如下：

```shell
/var/log/hsplog
{
	missingok
	daily
	copytruncate
	rotate 7
	notifempty
}
```

![image-20230426215043375](https://raw.githubusercontent.com/s2drag0n/Pictures/main/202304262150565.png)

日志轮替的原理是crond定时任务服务。

##### 内存日志

有一部分日志先写到了内存中，还没有写入文件，一般是内核日志。

journalctl 可以查看日村日志

常用的使用方式有

* journalctl
* journalctl -n 3 ##查看最新3条
* journalctl --since 19:00 --until 19:10:10
* journalctl -p err ##报错日志
* journalctl -o verbose ##日志详细内容
* journalctl _PID=1234 _COMM=sshd ##查看包含这些参数的日志（在详细日志中）
* journalctl | grep sshd

需要注意的是，重启后内存日志会被清空。

### 定制自己的Linux

#### linux启动流程

1. 首先Linux要通过自检，检查硬件设备有没有故障
2. 如果有多块启动盘，需要在BIOS中选择启动磁盘
3. 启动MBR中的bootloader引导程序
4. 加载内核文件
5. 执行所有进程的父进程、老祖宗systemd
6. 欢迎界面

在Linux启动流程中，加载内核文件时关键文件：

1. kernel文件：vmlinuz-3.10.0-957.el7.x86_64
2. initrd文件：initramfs-3.10.0-957.el.x86_64.img

#### mini Linux制作思路

1. 在现有的Linux系统(centos7.6)上加一块硬盘/dev/sdb，在硬盘上分两个分区，一个是/boot，一个是/，并将其格式化。需要明确的是，现在加的这个硬盘在现有的Linux系统中是/dev/sdb但是，当我们把东西全部设置好时，要把这个硬盘拔除，放在新系统上，此时，就是/dev/sda
2. 在/dev/sdb硬盘上，将其打造成独立的Linux系统，里面的所有文件是需要拷贝进去的
3. 作为能独立运行的Linux系统，内核是一定不能少，要把内核文件和initramfs文件也一起拷到/dev/sdb上以上步骤完成，我们的自制Linux就完成,创建一个新的linux虚拟机，将其硬盘指向我们创建的硬盘，启动即可

### 阅读Linux内核

1. C语言
2. 进程管理、内存管理、文件系统、驱动程序、网络
3. 纵向阅读，按照程序的执行顺序阅读；横向阅读，按照模块进行

### 内核升级

检测内核版本，显示可以升级的内核

`yum info kernel -q`

升级内核

`yum update kernel`

重启后查看当前安装的内核

`yum list kernel -q`

查看当前运行系统内核

`uname -a`

### 数据备份与恢复dump&restore

只有备份分区才支持增量备份

![image-20230428014143590](C:\Users\s2drag0n\AppData\Roaming\Typora\typora-user-images\image-20230428014143590.png)

![image-20230428014429233](C:\Users\s2drag0n\AppData\Roaming\Typora\typora-user-images\image-20230428014429233.png)

![image-20230428014753734](C:\Users\s2drag0n\AppData\Roaming\Typora\typora-user-images\image-20230428014753734.png)

### Linux可视化管管理

#### webmin

基于web的系统管理工具。

1. 下载地址：http://download.webmin.com/download/yum/

   也可以使用wget下载

2. 安装：`rpm -ivh webmin...(文件名)`

3. 重置密码：`/usr/libexec/webmin/changepass.pl /etc/webmin root passwd`

4. 修改webmin的端口号

   `vim /etc/webmin/miniserv.conf`

   将port=10000和llisten=10000修改为其他端口号6666

5. 启动webmin

   /etc/webmin/start

   /etc/webmin/restart

   /etc/webmin/stop

6. 防火墙开放端口

   `firewall-cmd --zone=public --add-port=6666/tcp --permanent`

   `firewall-cmd --reload`

   `firewall-cmd --zone=public --list-ports` 查看开放的端口号

7. 登录webmin

   通过http://ip:6666访问

#### bt宝塔面板

提升运维效率的服务器管理软件，支持一键LAMP/LNMP/集群/监控/网站/FTP/数据库//JAVA等多项服务器管理功能。

1. 安装

   `yum instll -y wget && wget -O install.sh http://download.bt.cn/install/install_6.0.sh && sh install.sh`

2. 安装成功后控制台会显示登陆地址、账号密码

3. bt default可以重置登陆地址、账号密码

### Linux面试题

等待观看

https://www.bilibili.com/video/BV1Sv411r7vd/?p=142&spm_id_from=pageDriver&vd_source=280794f09141eb6b4289ef941098e413

# 完结













