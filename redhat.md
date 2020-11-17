##第一章

1.man指令 /从上向下查找  ？从下向上查找  n下一个  N上一个

2.date指令 

​	date "+%Y-%m-%d %H:%M:%S" 按照yyyy-MM-dd HH:mm:ss格式显示系统时间

​	date -s "20201110 12:12:12" 将字符串转化为系统格式时间

​	date "+%j" 今天是今年的第几天

3.ps -aux查看进程信息

4.free  查看内存使用情况    free -h按照方便读的格式显示存储占用量

5.last命令用于查看所有系统的登录记录

6.history查看命令使用历史  history -c清空使用过的命令历史



7.tr命令 用于替换文本文件中的字符，格式为 tr [原始字符] [目标字符]

​	eg: cat passwd | tr [a-z] [A-Z]

8.wc命令 

​	wc -l 只显示行数

​	wc -w 只显示单词数

​	wc -c 只显示字节数

9.stat命令 用于查看文件的具体存储信息和时间等信息 格式为“stat 文件名称”

10.cut  命令用于按列提取文本字符 

​	cut -d: -f1 passwd    按照：分割词  然后取第一列数据

11.tar命令用于对文件进行打包压缩或解压

​	tar -czvf etc.tar.gz /etc  将/etc文件夹下的文件进行压缩

​	tar -xzvf etc.tar.gz -C /root/etc

​	-c 创建压缩文件

​	-x 解开压缩文件

​	-z用Gzip压缩或解压缩

​	-v显示压缩或解压的过程

​	-f目标文件名

​	-C指定解压到的目录

12.grep命令 用于在文本执行关键词搜索

​	grep 【选项】 【文件】

​	-c仅显示找到的行号

​	-i忽略大小写

​	-n显示行号

​	-v反向选择--仅列出没有“关键词”的行

​	-n 和 -v最为重要



##第二章

1.重定向 输入重定向中用到的符号及其作用

​	命令 < 文件    将文件作为命令的标准输入

​	命令 << 分界符     从标准输入中读入，直到遇见分界符才停止

​	命令 < 文件1 > 文件2    将文件1作为命令的标准输入并将标准输出到文件2

2.输出重定向中用到的符号及其作用

​	命令 > 文件    将标准输出重定向到一个文件中（清空原有文件的数据）

​	命令 2> 文件  将错误输出重定向到一个文件中（清空原有文件的数据）

​	命令 >> 文件  将标准输出重定向到一个文件中（追加到原有内容的后面）

​	命令 2>> 文件  将错误输出重定向到一个文件中（追加到原有内容的后面）

​	命令 >> 文件 2>&1

​	或者									将标准输出与错误输出共同写入到文件中（追加到原有内容的后面）

​	命令 &>>文件

3.管道符

​	格式 “命令A | 命令B” 作用是 把前一个命令原本要输出到屏幕的数据当作是后一个命令的标准输入

​	eg: grep "nologin" passwd | wc -l

​			ls -l /etc/ | more



##第三章 shell脚本编写

编写简单的shell脚本

​	#！脚本声明  用来告诉系统使用哪种shell解释器来执行该脚本

\	# 注释信息 对脚本功能和某些命令的介绍信息

​	bash example.sh 或者sh example.sh 可以运行写好的脚本

​	./example.sh 会提示权限不足，使用chmod u+x example.sh 可以赋权

​	

​	脚本中传参的方法  ./example.sh one two three four five six   变量之间用空格分隔

​	$0 对应当前shell脚本程序的名称

​	$#对应的是总共有几个参数，$*对应的是所有位置的参数值

​	$? 对应的是显示上一次命令的执行返回值

​	$1 $2 $3。。。。对应的分别是第N个位置上的参数值

​	

​	测试语句格式：[条件表达式] 两边均应有一个空格

​	文件测试所用的参数

​	-d 测试文件是否为目录类型

​	-e 测试文件是否存在

​	-f 判断是否为一般文件

​	-r 测试当前用户是否有权限读取

​	-w 测试当前用户是否有权限写入

​	-x 测试当前用户是否有权限执行

​	eg：[ -d test.sh ]

​			echo $?

​		如果输出0 表示正确 如果输出1表示不正确

逻辑语句用于对测试结果进行逻辑分析，根据测试结果可实现不同的效果。在shell终端中逻辑“与”的运算符号是&&，他表示当前命令执行成功后才会执行它后面的命令，因此可以用来判断文件是否存在。若存在则输出Exist字样

eg：[ -e /dev/cdrom ] && echo "Exist"



逻辑或，符号为“||” ，表示当前面的命令执行失败后才会执行他后面的命令，因此可以用来结合系统环境变量USER来判断当前登录的用户是否为非管理员身份

eg: [ $USER = root ] || echo "user"



逻辑非，符号为！，他表示把条件测试中的判断结果去相反值，

eg: [ ! $user = root ] || echo "administrator"



复合型判断语句

eg： [ ! $USER = root ] && echo "user" || echo "root" 类似于三目运算



整数运算符 只能用于数字对比

-eq 是否等于

-ne 是否不等于

-gt 是否大于

-lt 是否小于

-le 是否等于或小于

-ge 是否大于或等于



字符串比较运算符

= 比较字符串内容是否相同

!= 比较字符串内容是否不同

-z 判断字符串内容是否为空



for条件循环语句

​		for 变量名 in 取值列表

​		do

​				命令序列

​		done



​		for 用户名 in 列表文件

​		do

​				创建用户并设置密码

​		done



**   /dev/null是一个被称作Linux黑洞的文件，把输出信息重定向到这个文件等同于删除数据（类似于没有回收功能的垃圾箱），可以让用户的屏幕窗口保持简洁。



#!/bin/bash

read -p "Enter the users password:"  PASSWD

for UNAME in 'cat users.txt'

do 

​	id $UNAME &> /dev/null

​	if [ $? -eq 0 ]

​		then

​			echo "already exists"

​	else

​		useradd $UNAME &> /dev/null

​		echo "$PASSWD" | passwd --stdin $UNAME &> /dev/null

​		if [ $? -eq 0 ]

​			then

​				echo "$UNAME,create success"

​		else

​			echo "$UNAME,Create failure"

​		fi

​	fi

done



read 从输入行读取一个变量值  **-p 参数，允许在 read 命令行中直接指定一个提示。**

 

while条件循环语句

while 条件测试操作

do

​	命令序列

done



while 未猜中正确价格

do

​	反复猜测商品价格

done



#!/bin/bash

PRICE=$(EXPR $RANDOM % 1000)

TIMES = 0

echo "商品实际价格为0-999之间，猜猜看是多少"

while true

do

​	read -p "请输入您猜测的价格数目：" INT

​	let TIMES++

​	if [ $int -eq $PRICE];  then

​		echo "恭喜你答对了，实际价格是$PRICE"

​		echo "共猜测$TIMES次"

​		exit 0

​	elif [ $INT -gt $PRICE] ; then

​		echo "太高了"

​	else

​		echo "太低了"

​	fi

done



case 条件测试语句的语法结构

case 变量值 in

模式1）

​	命令序列1

​	;;

模式2）

​	命令序列2

​	;;

......

*)

​	默认命令序列

esac



case 输入的字符 in 

[a-z]|[A-Z])

​	提示为字母

​	;;

[0-9])	

​	提示为数字。

​	;;

​	.......

*)

​	提示为特殊字符

esac





3.4计划任务服务程序

echo "systemctl restart httpd" | at 23:30

at -l 如果想要查看设置好但还未只想的一次性计划任务

atrm 任务序号 删除任务

如果希望系统能够周期性的、有规律的执行某些具体的任务，那么Linux系统中默认启用的crond服务简直再适合不过了。创建、编辑计划任务的命令为“crontab -e”,查看当前计划任务的命令为“crontab -l”， 删除某条计划任务的命令为“crontab -r”。如果是管理员，可以在crontab命令中加上-u参数编辑他人的计划任务。

分、时、日、月、星期 命令，如果有字段没有设置，需要使用星号（*）占位。

分 取0~59的整数

时 取0~23的任意整数

日 取1~31的任意整数

月 取1~12的任意整数

星期 取0~7的任意整数，其中0与7均为星期日