# 目录

- [语法](#语法)

# 语法

- 传统if从句 -- 一条件表达式作为if条件
```
if[条件表达式]
then
 command
 command
 command
else
 command
 command
```

- 文件表达式
```
 if [ -f file] 如果文件存在
 if [ -d ...] 如果目录存在
 if [ -s file] 如果文件存在且非空
 if [ -r file] 如果文件存在且可读
 if [ -w file] 如果文件存在且可写 
 if [ -x file] 如果文件存在且可执行
```


- 整数变量表达式
```
 if [ int1 -eq int2 ] 如果int1等于int2
 if [ int1 -n2 int2 ] 如果不等于
 if [ int1 -ge int2 ] 如果 >=
 if [ int1 -gt int2 ] 如果 >
 if [ int1 -le int2 ] 如果<=
 if [ int1 -lt int2 ] 如果<
```

- 字符串变量表达式
```
 if [ $a = $b ] 如果string1等于string2 (字符串允许使用赋值号做等号)
 if [ $string1 != $string2] 如果string1不等于string2
 if [ -n $string ] 如果string 非空(非0),返回0(true)
 if [ -z $string ] 如果string 为空
 if [ $string ] 如果string非空,d 返回0
```


- 条件表达式引用变量要带$
```
 if [a = b];then
 echo equal
 else
 echo no equal
 fi
```

```
 [macg@machome ~]$ sh test.sh
 input a:
 5
 input b:
 5
 no equal (等于表达式没比较$a和$b,而是比较a,b,自然a!=b)

 改正:

 if [$a = $b];then
 echo equal
 else
 echo no equal
 fi

[macg@machome ~]$ sh test.sh
input a:
5
input b:
5
equal
```

-  -eq -ne -lt -nt只能用于整数，不适用于字符串，字符串等于赋值号=

```
[macg@machome ~]$ vi test.sh
echo -n "input your choice:"
read var
if [$var -eq "yes"]
then
echo $var
fi

[macg@machome ~]  $ sh -x test.sh
input your choice:
y
test.sh line 3:test:y:integer expression_r_r_r expected
                    期望整数形式，即-eq不支持字符串
```

-  =放在别的地方是赋值，放在if[]里就是字符串等于,shell里面没有==的，那是c语言的等于
  无空格的字符串，可以加 " ",也可以不加  

```
[macg@machome ~]$ vi test.sh
echo "input a:"
read a
echo "input is $a"
if [ $a = 123 ];then
echo equal123
fi

[macg@machome ~]$ sh test.sh
input a:
123
input is 123
equal123
```

-  = 作为等于时，其两边都必须加空格，否则失效
-  等号也是操作符，必须和其他变量，关键字，用空格格开(等号做赋值号时正好相反，两边不能有空格）

```

[macg@machome ~]$ vi test.sh

echo "input your choice:"
read var
if [ $var="yes" ]
then
echo $var
echo "input is correct"
else
echo $var
echo "input error"
fi  

[macg@machome ~]$ vi test.sh
echo "input your choice:"
read var
if [ $var = "yes" ]   在等号两边加空格
then
echo $var
echo "input is correct"
else
echo $var
echo "input error"
fi


[macg@machome ~]$ sh test.sh
input your choice:
y
y
input is correct
[macg@machome ~]$ sh test.sh
input your choice:
n    
n
input is correct 
输错了也走then,都走then,为什么?
因为if把$var="yes"连读成一个变量，而此变量为空，返回1，则走else   [macg@machome ~]$ sh test.sh
input your choice:
y
y
input error
[macg@machome ~]$ sh test.sh
input your choice:
no                       
no
input error
一切正常
```

- if [ $ANS ] 等价于 if [ -n $ANS ]
  如果字符串变量非空(then),空(else)

```
echo "input your choice:"
read ANS

if [ $ANS ]
then 
echo no empty
else
echo empty
fi

[macg@machome ~]$sh test.sh
input your choice:     回车

empty         说明‘回车’就是空串
[macg@machome ~]$sh test.sh
input your choice:
34
no empty

```

- 整数条件表达式,大于，小于,shell里没有>和<,会被当作尖括号，只有 -ge -gt -le lt

```
[macg@machome ~]$ vi test.sh]

echo 'input a:'
read a
if [ $a -ge 100 ];then
echo 3bit
else
echo 2bit
fi

[macg@machome ~]$ sh test.sh
input a:
123
3bit
[macg@machome ~]$ sh test.sh
input a:
20
2bit

```

- 整数操作符号 -ge -gt -le -lt 别忘了加-   
```
if test $a ge 100;then

[macg@machome ~]$ sh test.sh
test.sh: line 4: test: ge: binary operator expected

if  test $a -ge 100 ; then
[macg@machome ~]$ sh test.sh
input a:
123
3bit
```

- ========================逻辑表达式  

```
逻辑非 !  条件表达式的相反
if [ ! 表达式 ]
if [ ! -d $num]    如果不存在目录$num

逻辑与 -a        调价表达式的并列
if [ 表达式1 -a 表达式2 ]

逻辑或  -o
if [ 表达式1 -o 表达式2  ]

逻辑表达式
   表达式与前面的= != -d -d -x -ne -eq -lt等合用
   逻辑符号就正常的接其他表达式,没有任何括号(),就是并列

if[ -z "$JHHOME" -a -d $HOME/$num ]
    注意逻辑与-a与逻辑或-o很容易和其他字符串或文件的运算符号搞混了   

```

- 最常见的赋值形式，赋值前对=两遍的变量都进行评测  
  左边测变量是否为空，右边测目录(值)是否存在(值是否有效)

```
[macg@mac-home ~]$ vi test.sh
:
echo "input the num:"
read num
echo "input is $num"

if [ -z "$JHHOME" -a -d $HOME/$num ] 如果变量$JHHOME为空，且$HOME/$num目录存在
then 
JHHOME=$HOME/$num        则赋值
fi

echo "JHHOME is $JHHOME"

[macg@mac-home ~]$ sh test.sh
input the num:
ppp
input is ppp
JHHOME IS

目录-d $HOME/$num 不存在,所以$JHHOME没被then赋值

[macg@mac-home ~]$ mkdir ppp
[macg@mac-home ~]$ sh test.sh
input the num:
ppp
input is ppp
JHHOME is /home/macg/ppp
```

- 一个 -o的例子,其中却揭示了"="必须两遍留空格的问题  
```
echo "input your choice:"
read ANS

if [ $ANS="Yes" -o $ANS="yes" -o $ANS="y" -o $ANS="Y" ]
then
ANS="y"
else
ANS="n"
fi

echo $ANS

[macg@machome ~]$ sh test.sh
input your choice:
n
y
[macg@machome ~]$ sh test.sh
input your choice:
no
y

为什么输出不是yes,结果仍走了then 
因为=被连续了,成了变量$ANS="YES",儿变量又为空,所以走else了


[macg@machome ~]$ vi test.sh
echo "input your choice:"
read ANS echo "input choice:"
read ANS

if [ $ANS = "Yes" -o $ANS = "yes" -o $ANS = "y" -o $ANS = "Y" ]
then
ANS='y'
else
ANS='n'
fi

echo $ANS

[macg@machome ~]$ sh test.sh
input your choice:
no
n
[macg@machome ~]$ sh test.sh
input your choice:
yes
y
[macg@machome ~]$ sh test.sh
input your choice:
y
y
```

-  =========================以test条件表达式作为if条件  

```
  if test $num -eq 0 等价于 if [ $num -eq 0 ]

  test 表达式，没有 [ ]
  if test $num -eq 0
  then
  echo "try again"
  else
  echo "good"
  fi

```

```
  man test
  [macg@machome ~]$ man test
[(1)                             User Commands                            [(1)

SYNOPSIS
       test EXPRESSION
       [ EXPRESSION ]


       [-n] STRING
              the length of STRING is nonzero          -n和直接$str都是非0条件

       -z STRING
              the length of STRING is zero

       STRING1 = STRING2
              the strings are equal

       STRING1 != STRING2
              the strings are not equal

       INTEGER1 -eq INTEGER2
              INTEGER1 is equal to INTEGER2

       INTEGER1 -ge INTEGER2
              INTEGER1 is greater than or equal to INTEGER2

       INTEGER1 -gt INTEGER2
              INTEGER1 is greater than INTEGER2

       INTEGER1 -le INTEGER2
              INTEGER1 is less than or equal to INTEGER2

       INTEGER1 -lt INTEGER2
              INTEGER1 is less than INTEGER2

       INTEGER1 -ne INTEGER2
              INTEGER1 is not equal to INTEGER2

       FILE1 -nt FILE2
              FILE1 is newer (modification date) than FILE2

       FILE1 -ot FILE2
              FILE1 is older than FILE2

       -b FILE
              FILE exists and is block special

       -c FILE
              FILE exists and is character special

       -d FILE
              FILE exists and is a directory

       -e FILE
              FILE exists                                 文件存在

       -f FILE
              FILE exists and is a regular file     文件存在且是普通文件

       -h FILE
              FILE exists and is a symbolic link (same as -L)

       -L FILE
              FILE exists and is a symbolic link (same as -h)

       -G FILE
              FILE exists and is owned by the effective group ID

       -O FILE
              FILE exists and is owned by the effective user ID

       -p FILE
              FILE exists and is a named pipe


       -s FILE
              FILE exists and has a size greater than zero

       -S FILE
              FILE exists and is a socket

       -w FILE
              FILE exists and is writable

       -x FILE
FILE exists and is executable
```

- ================if简化语句=======================  

```
最常用的简化 if 语句

 && 如果是"前面",则“后面”
 [ -f /var/run/dhcpd.pid ] && rm /var/run/dhcpd.pid 检查文件是否存在,如果存在就删掉

 || 如果不是前面，则后面
 [ -f /usr/sbin/dhcpd ] || exit 0 检查文件是否存在，如果存在就退出
```

- 用简化 if 和 $s1,$s2,$s3来检测参数,不合理就调用help  

```
  [ -z "$1" ]&& help 如果第一个参数不存在 (-z 字符串长度为0)
  [ "$1" = "-h" ] && help   如果第一个参数是-h，就显示help


例子
#!/bin/sh

[ -f "/etc/sysconfig/network-scripts/ifcfg-eth0" ] && rm -f /etc/sysconfig/network-scripts/ifcfg-eth0
cp ifcfg-eth0.bridge /etc/sysconfig/network-scripts/ifcfg-eth0

[ -f "/etc/sysconfig/network-scripts/ifcfg-eth1" ] && rm -f /etc/sysconfig/network-scripts/ifcfg-eth1
cp ifcfg-eth1.bridge /etc/sysconfig/network-scripts/ifcfg-eth1

[ -f "/etc/sysconfig/network-scripts/ifcfg-eth0:1" ] && rm -f /etc/sysconfig/network-scripts/ifcfg-eth0:1
```
