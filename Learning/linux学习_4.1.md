# 4.1 命令学习

* ls命令 选项\[-ald\][文件或目录]

---

ls -a：显示所有文件
ls -l：显示文件7个信息：
ls -d：查看目录属性
ls -i：查看文件id号
ls -h：显示文件实际大小

---

所有者(user)：只有一个，可以转变

所属组(group)：只有一个，

其他人(other)：除了所有者和所有组的其他人



文件类型(十个字节，如： -rw-r--r--)

\-: 二进制文件 

d: 目录  

l: 软连接文件

---

r: read

w: write

x: execute 

---
第2到第4个字符：rw-  表示**user**可以r&w；
第5到第7个字符：r--  表示**group**可以r&w；
第8到第10个字符：r--  表示**other**可以r&w。

---
* mkdir
	* mkdir [目录] 创建目录
	* mkdir -p [目录] 连续创建目录

---

* cd 
	* cd [目录] 切换到目录
	* cd .. 切换到上一级目录

---

* pwd
	* 显示当前目录全部路径

---

* rmdir
	* rmdir [目录] 删除空目录

---

* cp
	* cp [原文件\]\[目标目录\] 将原文件复制到目标目录下
	* cp -r  [原目录\]\[目标目录\] 复制原目录到目标目录下（可改名）
	* cp -p  [原目录\]\[目标目录\] 保留文件属性
	复制同时能改名

---

* mv
	* mv [原文件或目录\]\[目标目录\] 将原文件或目录剪切到目标目录下（可改名）

---

* rm
	* rm [文件] 删除文件
	
	* rm -r [目录] 删除目录
	
	* rm -f [文件或目录] 强制删除（不会询问）
---

## 4.2 权限管理命令

---

* chmod  (user & root能更改文件权限)
	* chmod [{ugoa}{+-=}{rwx}]\[文件或目录\] 用户 加减等 权限
	* 权限用数字表示：
		> r:4
		> w:2
		> x:1
		> 9个字符权限用3个数字表示：rwxrw-r--：7 6 4
	* chmod [数字] \[文件名\]  按数字修改权限
	* chomd -R [数字] \[文件名\]  按数字修改目录及内部所有文件权限

---

* file & directory
	* file: 
		> r: cat/more/head/tail/less
		> w: vim
		> x: scipt command
	* directory:
		> r: ls
		> w: touch/mkdir/rm/rmdir
		> x: cd
		对文件没有写权限，但对文件所在目录有写权限同样可以删除。（子承父业）

---

* chown （改变文件所有者）只有root用户可以做
	* chown [用户]\[文件或目录\]

---

* chgrp （改变文件所属组）只有root用户可以做
	* chgrp [用户组]\[文件或目录\]

---

注：
> 一个用户可以有很多个所属组，但有一个缺省组
> 
> Linux默认新建的文件不具有可执行文件，目录可以

---

* umask [-S]查看缺省文件权限

	* umask [权限数字] 更改缺省文件权限，如umask 077: -rwx------

---

## 4.3 文件搜索命令
---

* find 文件搜索命令
	* find [搜索范围]\[匹配条件\] 注意区分大小写
	* -name 按名字搜索
		* find /etc -name init 在/etc目录下找名字为init的文件（精确搜索）
		* find /etc -name \*init\*  在/etc目录下找名字包含init的文件（模糊搜索）
		* find /etc -name init\*???  在/etc目录下找名字包含init开头后面为3个字符的文件（模糊搜索）
	* -iname 按名字搜索，不区分大小写 
	* -size (1数据块=512字节=0.5K)
		* +n 查找大于n的文件
		* -n
		* n 
	* -user(-group) 按所有者（所属组）搜索
	* -cmin（属性更改）(-amin（访问）, -mmin（内容更改）) [+5,-5,5] 5min内（外）修改过的文件
	* -type (f 文件,d 目录 ,l 软链接)
	* -inum 根据i节点查找(可用于寻找是否有硬链接)
	* -a(-o) 两个查找条件同时满足（满足其一）
	* \+ -exec 命令 {} \; 表示找到文件后执行某个命令；如：find /etc -name init\* -a -type f -exec ls -l {} \;

---

* locate 快速文件查找(类似于windows的Everything)
	* locate [文件]
	* updatedb 手动更新资料库，不能找到/tmp的文件
	* locate -i [文件] 不区分大小写

---

* which 查找命令所在目录和别名信息
	* which [命令] 

---

* whereis 搜索命令所在目录和帮助文档路径
	* whereis [命令]

---

* grep 文件内搜索包含内容的行
	* grep [内容] \[文件名\]
		* -i 不分区大小写
		* -v 排除指定字符串；如：grep -v ^# /etc/inittab
		* \#开头表示表述信息

---
## 4.4 帮助命令
---
* man [命令或配置文件名称（不需要绝对路径）] 帮助信息（主要看NAME）
	* 1 表示命令的帮助
	* 5 表示配置文件的帮助
	* man 1 [命令]
	* man 5 [配置文件]

---
* whatis [命令]
* apropos [配置文件]
* 命令 --help
* info [命令]
* help [内置命令] （内置命令是找不到文件路径的命令(which/whereis)）

---
## 4.5 用户管理命令

---
* useradd [用户名] 创建账号
* passwd [用户名] 修改密码
* who 简短信息
* w 详细信息

---

## 4.6 压缩与解压

---
* gzip
	* gzip [文件] 只能压缩文件，不保留源文件
	* gunzip [压缩包]/gzip -d

---
* tar：打包目录
	* tar -cf [压缩包文件名.tar] \[需要打包目录\] 打包不压缩
	* tar -xf [压缩包文件名.tar] 取消打包
	* tar -zcf [压缩包文件名.tar.gz] \[需要打包压缩目录\]
	* tar -zxf  [压缩包文件名.tar.gz] 解压缩
	* -x 解包
	* -v 显示详细信息
	* -f 压缩目录
	* -z 

---

* zip：windows与linux通用的格式
	* zip -r  [压缩包文件名.zip] \[需要压缩的文件或目录\] 压缩
	* unzip [压缩包文件名.zip]解压缩

---
* bz2：压缩比很高
	* bzip2 -k [文件] （\k表示保留源文件）
	* bunzip2  [压缩包文件名.bz2]解压
	* tar -cjf [压缩包文件名.tar.bz2] \[需要打包压缩目录\] 压缩
	* tar -xjf  [压缩包文件名.tar.gz] 解压缩
---
## 4.7 网络命令
---
* write: 给**在线**用户写
	* write [用户名]
	* crol + D 结束

* wall: 给所有用户写信息（广播信息）
	* wall [内容]

* ping：网络畅通性
	* ping [ip地址]
	* ping -c [数字] \[ip地址\]: 只ping几行

* ifconfig：查看网络驱动

* mail：发送电子邮件
	* mail [用户名]：发信
	* mail：查看信箱
		* help
			* 序号
			* h回看目录
			* d序号：删除邮件
			* q：退出

* last：查看登录信息
	* lastlog
		* lastlog -u [ID] 仅查看某一用户的登录信息

* traceroute: 访问网络节点（可看各个IP）

* netstat: 查看网络相关信息
	* netstat [选项]：
		* -t：TCP协议：类似打电话
		* -u：UDP协议：类似于发短信
		* -l：监听
		* -r：路由
		* -n: 显示IP地址和端口号
	* netstat -tlun： 查看监听端口
	* netstat -an：查看所有网络连接
	* netstat -rn: 查看路由表

* setup: 永久修改IP

* mount: 挂载（目录要先创建（mkdir /mnt/cdrom））
	* mount /dev/sr0 /mnt/cdrom/ : 挂载光盘
	* umount /dev/sr0：弹出光盘（回根目录再卸载）

---
## 4.8 关机和重启
---

* shutdown: 关机(先断开服务再关机或重启，服务器只能重启不能关机！！！)
	* shutdown [选项] \[时间\]：选择时间关机或重启（now,hh:mm）
		* -c：取消前一个关机命令
        * -h：关机
        * -r：重启
* reboot: 重启
* init：
	init 0~6：0 关机，6 重启。（5：X11，图形界面运行级别）
	runlevel: 查看运行级别
* logout： 退出登录


## 5.1 Vim常用操作

* vi [filename]
	* 命令模式  插入模式 编辑模式 
	* 插入模式： 
		* a 光标字符后插入；A行尾
		* i 光标字符前输入； O行首
		* o光标下一行输入
	* : set nu 添加行号  
	* :n  定位到某行
	* x 删除光标所在字符
	* dd 删除光标所在行
	* yy + p 复制粘贴
	* dd + p 剪切
	* R 替换光标字符
	* u 恢复上一步操作
	* :w 保存修改
	* :wq 保存退出(ZZ)
	* :q! 不保存退出
	* :wq! 强制保存修改

* :r ![命令]
* 快捷键
	* :map ^P I#\<ESC\>   添加快捷键(^P表示crol+v+p)
	* :ab [a]\[b\] 敲入a变成b
	* 永久生效可以写到 /.vimrc 配置文件里

## 6.1 软件安装
---
* 软件分类： 
	* 源代码包（C语言）：可以看到源代码，可以自由配置安装内容，效率高
	* 二进制包（rpm包）：安装快，不能看到源代码

* rpm包管理：
	1. 命名规则： 了解
		* 包名、包全名:
			* 安装和升级时使用包全名；
			* 搜索已经安装的包（执行、卸载）使用包名；
	2. 依赖性：
		* 树形依赖：a, b, c
		* 环形依赖：a, b, c, a
		* 模块依赖：以.so.n(n为数字)结尾，www.rpmfind.net
	3. 安装：
		命令： rpm -ivh [包全名]
			-i 安装
			-v 显示详细信息
			-h 显示进度
	4. 升级：
		命令： rpm -Uvh [包全名]
		
	5. 卸载：
		命令： rpm -e [包名]
		
	6. 查询：
		命令：rpm -q [包名]
			rpm -qa [包名]: 列出所有安装的包
			rpm -qi [包名]: 查看已安装软件包详细信息
			rpm -qip [包全名]: 查看未安装软件包详细信息
			rpm -ql [包名]: 查看已安装软件包位置
			rpm -qlp [包全名]: 查看未安装软件包打算安装位置
	7. 校验：
		命令：rpm -V [已安装的包名]
	
	8. 安装包文件提取

* yum包安装：
	1. IP配置
		* setup 配置
		* 修改配置文件 vi /etc/sysconfig/network-scripts/ifcfg-eth0
		* service network restart
	2. 网络yum源

	3. 命令
		* 查询  
			* yum list
			* yum search [包名]

		* 安装
			* yum -y install [包名]：（install 安装  -y 自动回答yes）

		* 升级
			* yum -y update [包名]：不加包名会升级所有软件

		* 卸载
			* yum -y remove [包名]：不加包名会升级所有软件
		
		* 软件包组安装
	
	4. 光盘yum源搭建：
			*挂载
			*关闭网络yum源
			*配置media源
				1. 改路径
				2. 注释掉其他两个路径
				3. enable=1

* 创建帐号
useradd [帐号]
passwd [帐号]

