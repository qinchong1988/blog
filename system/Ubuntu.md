# 文件颜色
蓝色-目录<br>
绿色-可执行文件<br>
红色-压缩文件<br>
浅蓝色-链接文件<br>
灰色-其它文件

#系统命令

1. lsb_release -a <br>
>No LSB modules are available.<br>
Distributor ID:	Ubuntu<br>
Description:	Ubuntu 13.10<br>
Release:	13.10<br>
Codename:	saucy<br>

2. env 查看系统的环境变量


# Shell
Shell有很多，但常用的就几种

|Shell名称 |开发者 |命令名称|
--------------------------
|Bourne    |S.R.Bourne| /bin/sh|
|C        |Bill Joy|/bin/csh|
|Kom    |David|  /bin/ksh|

Shell 的修改
直接输入 :
chsh -s 输入新的shell 如:/bin/csh

查看历史命令
history

追踪路由
traceroute www.baidu.com
查看路由表
route

查看ip情况
ifconfig

Linux 网络环境配置
第一种方法：
（1）用root身份登陆，运行setup命令进入到text mode setup utiliy 对网络进行配置，
这里可以对ip，子网掩码，默认网关，dns的设置。
（2）这时网卡的配置没有生效，运行/etc/rc.d/init.d/network restart 命令我们刚才的
设置才生效.

第二种方法:
(1) ifconfig eth0 x.x.x.x对网卡进行设置
(2）ifconfig eth0 network x.x.x.x对子网掩码设置
对广播地址和dns使用默认的。
注意：这样配置网络将会立即生效，但是是临时生效，重启就没了。

第三种方法：
(1).修改/etc/sysconfig/network-scripts/ifcfg-eth0
这个文件各个属性可以修改。包括ip,子网掩码，广播地址，默认网关。
(2).这时网卡的配置没有生效，运行
/etc/rc.d/init.d/network restart命令我们刚做的设置才生效
这种方法是最底层的修改方法

任务调度的使用crontab

1.设置任务.
  crontab -e
2.每隔一定时间去执行 date > /home/mydate1
	1)希望，每天凌晨2:00去执行 date >> /home/mydate2
	可以在crontab -e中加入
	0 2 * * * date >> /home/mydate2
	2)希望，每分钟
	* * * * * date >> /home/mydate2
调度文件的规则：
	分钟 每小时中得第几分钟执行  0-59
	小时 每日的第几小时执行      0-23
	日期 每月的第几天执行        1-31
	月历 每年的第几个月执行      1-12
	星期 每周的第几天执行        0-6
 	invalid data will not execute
3.怎样去调用多个任务？
    1).在crontab -e 中直接写.(不推荐)
    2).可以把所有的任务，写入到一个可执行文件(Shell编程)(很好)
    * * * * * /root/mytask.sh
4.如何终止任务调度：
    crontab -r ：终止任务调度
    crontab -l : 列出当前有那些任务调度

ps -aux | more

终止进程kill/killall
终止某个进程:kill 进程号
kill -9 进程号

监控网络状态信息：
显示网路统计信息的命令netstat
netstat -anp

一些命令
cp -r dir1 dir2 递归复制命令(复制子目录信息)
mv :移动文件和改文件名
rm :删除文件和目录
rm -rf * 删除所有内容（包括目录和文件）
ln -s 源 目标
ls -s /etc/inittab inittab

linux 启动过程分析
runlevel命令，可以查看当前的运行级别
linux系统启动过程如下：
a) BIOS自检
b) 启动GRUB/LILO
c) 运行LINUX内核并检测硬件
d) 运行系统的第一个进程init
e) init读取系统引导配置文件/etc/inittab中的信息进行初始化
f) /etc/rc.d/rc.sysinit系统初始化脚本
g) /etc/rc.d/rcX.d/[KS]* -根据运行级别X配置服务
    终止以"K"开头的服务
    启动以"S"开头的服务
h) /etc/rc.d/rc.local 执行本地特殊配置
i) 其他特殊服务




