

#	Basic Shell Script



## if

```bash
#!/bin/bash
if command
then
	commands
fi
```

```bash
#!/bin/bash
if command; then
	commands
fi
```

```bash
#!/bin/bash
if command
then
	commands
else
	commands
fi
```

## test condition

`if test condition`

`if [ condition ]`方括号定义了测试条件。注意，第一个方括号之后和第二个方括号之前必须加上一个空格，
否则就会报错。 

### 数值比较

`-eq``-ge``-le``-gt``-lt``-ne`

**bash shell 只能处理整数**

###	字符串比较

`=``!=``<``>` **大于号小于号必须转义**，否则作为重定向了

`-n`长度是否为非0 not zero

`-z`长度是否为0 is zero

sort处理大写字母方法和test命令相反，**test命令中大写字母被认为小于小写**

## 文件比较

`-d`exist and direction?

`-e`exist?

`-f`exist and file?

`-r`exist and read?

`-s`exist and not-empty?

`-w`

`-x`

`-O`is current user's file?

`-G`same group with current user

`-nt`new than

`-ot`old than

## if-then 高级特性

`if (( expression ))` 计算特性

`val++`

`val--`

`&`

`|`

`&&`

`||`

`if [[ expression ]]` 字符特性

在上面的脚本中，我们使用了双等号（ == ）。双等号将右边的字符串（ r* ）视为一个模式，
并应用模式匹配规则。双方括号命令 $USER 环境变量进行匹配，看它是否以字母 r 开头。如果是
的话，比较通过，shell会执行 then 部分的命令。 

## case

```bash
#!/bin/bash
case $USER in
rich | barbara)
	commands;;
testing)
	commands;;
jesssica)
	commands;;
*)
	commands;;
esac
```

## for

```bash
for var in list
do
	commands
done
```

`'`会让list中的词作为一个item

列表中读取变量，注意更改字段分隔符， `internal field separator`

`IFS=$'\n'`**注意有美元符号还有引号**

`if [ -d "$file"]`**注意有双引号**

c语言风格的for

```bash
for (( i = 1; i <= 10; i++ ))
do
	command
done
```

```bash
for (( a=1, b=10; a <= 10; a++, b-- ))
do
	commands
done
```

## while

```bash
while [ $var1 -gt 0 ] # while $var1 is great than 0 do the loop
do
	echo $var1
	$var1=$[ $var1 - 1 ]
done
```

```bash
	$var1=$[ $var1 - 1 ]
```

## until

```bash
until [ $var1 -eq 0 ] # until $var1 is equal to zero *end the loop
do
	echo $var1
	$var1=$[ $var1 - 1 ]
done
```

**shell会执行指定的多个测试命令，只有在最后一个命令成立时停止。** 

## break

break is break the hole loop

`break 2` is to break outer loop, when you want to break outer loop in inside loop use this command

`break` is same to `break 1`

内部循环里的 for 语句指明当变量 b 等于100时停止迭代。但内部循环的 if-then 语句指明当变量 b 的值等于5时执行 break 命令。注意，即使内部循环通过 break 命令终止了，外部循环依然继续执行。 

## continue

continue 命令可以提前中止某次循环中的命令，但并不会完全终止整个循环。可以在循环内部设置shell不执行命令的条件。这里有个在 for 循环中使用 continue 命令的简单例子。 

**continue 命令时，它会跳过剩余的命令。如果你在其中某个条件里对测试条件变量进行增值，问题就会出现。** 

## done

```bash
done > output.txt
```

