### 1.mkdir 创建目录/文档

​	在当前目录下创建1000个目录 新建文件夹0到新建文件夹1000
​		   命令  : mkdir 新建文件夹{1..1000}

​	常用选项：
​    	-p ：逐层创建目录
​    		mkdir -p One/Two/Three/Go

​	如果中间目录不存在,直接创建



### 2.touch

####     		1.作用

​        	1.文件不存在 -> 创建

​			2.文件存在 -> 用系统时间更新文件修改时间

####     		2.格式 ：touch 文件名1 文件名2 文件名3 ...

### 3.rm ：删除文件/目录

#### 			1.rm 选项 文件/目录

​		-r ：删除全部文件/目录
​        -f ：强制删除,不给任何提示 ---> 无法删除文件夹
​        -i ：删除前给提示(y代表yes,n代表no) ---> 无法删除文件夹
​        	rm -rf 文件名/目录名
​			删除根目录下的/a.txt  /b.txt
​			rm -rf /a.txt /b.txt
​			rm -r admin{1..1000}

​			*匹配所有
​			**^a匹配以a开头的文件**
​         	   ! 取反
​	创建a{1..1000}的文件,删除除了a50以外的所有文件
​	/log/201801.sql.log 删除除了2018年1月份以外的所有文件
​		rm -rf 201802..sql.log ...  一个一个删除
​		rm -rf !(201801.sql.log)
​	/ a{1..1000}   不要执行rm -rf !(a50)  # 防止其他文件删除
​	删除除了a10和a20以外的文件
​		rm -rf !(a10|a20)

### 4.>   重定向  # 会覆盖已有的内容

​	echo 13087508351 > day1
​	>> 追加重定向 # 不会覆盖已有的内容,将插入的内容插至末行
​	仅适用与追加一行
​	echo 13087508351 >> day1

### 5.cat 查看制定文件里的内容

​	把/etc下的 passwd 重定向到 /root/pass
​		cat /etc/passwd > /root/pass
​	把/etc下的 gshadow 追加重定向到 /root/pass
​		cat /etc/gshadow > /root/pass

​	echo 123456 > a
​	echo 789456 > b
​	cat a >> b  # 把a里面的文档内容追加到b里面,a的文档仍在

### 6.cp 复制

​	cp /源文件路径/名称 /目标文件路径/[名称] # 不设置名称默认为原文件名
​	cp -p 复制的时候保证源文件权限不变
​	cp -rp /etc/* /opt/  (递归复制目录及其子目录内的所有内容)

### 7.mv 剪切

​	在相同路径下面属性重命名
​	把 /etc/gshadow 复制到 /opt
​		cp /etc/gshadow /opt/
​	把 /opt/gshadow 移动到 /root/gsha
​		mv /opt/gshadow /root/gsha
​	把/root/gsha 重命名 test
​		mv /root/gsha /root/test

### 8.文件查找

​		less test 以行显示	
​		more test 以页显示
​		head -5 test # 查看前5行
​		tail -5 test # 查看后5行
​		显示后10行的前5行
​			tail -10 Linux/day01.txt | head -5

### 9.which 查找命令路径

​	[root@localhost ~]# which ls
​	alias ls='ls --color=auto'
​		/usr/bin/ls

### 10.find 	查找文件

​	find 路径 选项1 选项2
​	find -name # 按照文件名查找
​	find -iname # 按照文件名(匹配大小写)查找
​	find -type # 按类型查找

​						-d ：目录

​						-p：管道文件

​						-f：普通文件

​						-i ：符号链接文件

​	find -mtime # 按时间查找
​	find -user # 按用户查找
​	find -group # 按照组名查找

​	find -perm # 根据文件权限查找

​		find -perm 777: 查找权限为777(rwx-rwx-rwx)的文件

​	find -size # 按照大小查找  +4G -4G 4G(大于,小于,等于)
​         -a 
​         -or 
​         -inum 以i节点信息去查找
​	例:
​		find / -name a  # 查找/目录下 a开始的文件
​		find / -name a -type f文件 | d目录   
​		find -size +4G
​		find -mtime +10 # 10天前的文件   + 代表 加号后面数字天之前的文件  - 代表 减号之后数字天之内的文件
​		find / -user student

### 11.grep 	查找文件内容

​	-v 取反
​	-o root 只显示root
​	grep root /etc/passwd  # 显示包含root的信息
​	grep ^root /etc/passwd  # 显示以root开头的信息
​	grep root$ /etc/passwd  # 显示以root结尾的信息
​	grep -o root /etc/passwd # 查找出来的root 一行一行显示出来
​	grep -v root /etc/passwd # 查找不包含root的信息
​	grep 5$ a.txt # 显示以5结尾的信息 

### 12.alias 别名: 帮助我们简化命令(默认本次有效)

​	unalias -a: 取消别名(没有-a,默认取消所有别名)
​	ssh: 远程 ssh root@192.168.4.5
​	永久性设置别名
​		vim /etc/bashrc 
​		第二行
​		alias goa="ssh -X root@192.168.4.5"
​		alias hang="init 0"
​		bash # 刷新

### 13.hostname 查看主机名

​		hostname name # 设置主机名
​		vim /etc/hostname里面更改
​		reboot #重启后主机名生效

### 14.linux tty终端 ctrl + alt + F(1-5)  # 切换终端

​	0:	halt 关机
​	1:	单用户模式,单用户模式只有系统管理员才可以进入
​	2:	不具备网络文件系统功能的多用户命令行模式.
​	3:	具有网络文件系统功能的多用户命令行模式
​	4:	保留使用
​	5:	具备网络功能的xwindows模式.系统初始化直接进入图形界面.适合初学者使用
​	6:	关闭所有运行的程序并重新启动
​	halt 关机
​	init 0 关机  init (1-6)

### 15.tar ：打包并压缩

####     1.格式

​    	tar -zcvf 压缩包名字.tar.gz 需要压缩文件/目录
​    	-z ：用gzip对包进行压缩
​    	-c ：创建包(create)
​    	-v ：显示明细(verbose)
​    	-f ：file

####     2.解压缩

​    	tar -zxvf 压缩包名字.tar.gz -C 路径
​    	-C ：指定解压路径,不写默认解压到当前