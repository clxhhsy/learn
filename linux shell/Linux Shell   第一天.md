# 开始学习Linux Shell 
##### Shell的格式
```
	#!/bin/sh
	#comments
	your commands go here
```
> \#!是一个约定的标记，它告诉系统这个脚本需要什么解释器来执行，如果不加会报错的。  

#### shell脚本执行的两种方式
##### 一、作为可执行程序
> 例：有一个文件为test.sh  

```
	chmod +x ./test.sh #使脚本具有可执行权限
	./test.sh	#执行脚本
```  

##### 二、作为解释器参数
	/bin/sh test.sh  
> 此种方式不需要再脚本文件的开头指定脚本解释器。  

## shell变量
### 定义变量
定义变量时，变量名不加'$',如：`variableName="value"`
> 注意：<font color="#DC143C">变量名和'='号之间不能有空格</font>
> 命名规则：
* 首个字符必须为字母
* 中间不能有空格，可以使用下划线'_'
* 不能使用标点符号
* 不能使用bash里的关键字(可以使用help命令查看保留关键字) 

### 使用变量
使用一个定义过的变量，只要在变量前加'$'即可。如：`name="lily" echo $name echo ${name}`
> 推荐给变量加上括号

### 只读变量
	name="lisi"
	readonly name
此时，name变为一个只读变量，后面就不能再给变量赋值，否则会报错。

### 删除变量
	name="lisi"
	unset name
	echo $name
变量被删除后不能再使用；unset不能删除只读变量

### 变量类型
1. 局部变量
局部变量在脚本或命令中定义，仅在当前shell实例中有效。
2. 环境变量
所以的程序，包括shell启动程序，都能访问环境变量。
3. shell变量
shell变量是由shell程序设置的特殊变量。

#### 特殊变量列表
|变量|含义|
|:---:|:----|
|$0|当前脚本的文件名|
|$n|传递给脚本或函数的参数。n是一个数字，表示第几个参数。|
|$#|传递给脚本或函数的参数个数。|
|$*|传递给脚本或函数的所有参数|
|$@|传递给脚本或函数的所有参数。被双引号包含时，与$*稍有不同|
|$?|上个命令的退出状态，或函数的返回值|
|$$|当前shell进程ID。对于shell脚本，就是这些脚本所在的进程ID|

##### $*和$@的区别
$*和$@都表示传递给函数或脚本的参数，不被双引号包含时，都以$1,$2的形式输出所有的参数
但是，当他们被双引号包含时，$*会将所有的参数作为一个整体，以"$1 $2 ... $n"的形式输出所有的参数；$@会将各个参数分开，以"$1""$2"的形式输出所有参数
```
	#!/bin/sh
	echo "\$*=" $*
	echo "\"$*\"=" "$*"

	echo "\$@=" $@
	echo "\"\$@\"=" "$@"

	echo "print each param from \$*"
	for var in $*
	do
		echo "$var"
	done
	
	echo "print each param from\$@"
	for var in $@
	do 
		echo "$var"
	done
	
	echo "print each param from \"\$*\""
	for var in "$*"
	do 
		echo "$var"
	done
	
	echo "print each param from \"\$@\""
	for var in "$@"
	do 
		echo "$var"
	done
```

```
./test.sh "a" "b" "c" "d"
$*= a b c d
"$*"= a b c d
$@= a b c d
"$@"= a b c d
print each param from $*
a
b
c
d
print each param from $@
a
b
c
d
print each param from "$*"
a b c d
print each param from "$@"
a
b
c
d
```

### 退出状态
退出状态即为上一个命令执行后的返回结果

```
$./test.sh aaa bbb
$echo $?
0
$
```