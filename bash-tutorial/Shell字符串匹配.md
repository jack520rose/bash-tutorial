## Shell字符串匹配

### grep命令

使用`grep命令`的`-E` 、`-o`参数进行实现，`-o`选项表示只输出匹配的部分，`-E`选项表示使用扩展正则表达式。

```shell
fastq=J-20230810-680-1-123808018_raw_2.fq.gz
# 提取样本编号
echo $fastq|grep -oE [0-9]{9} 
```

### sed命令

使用`sed命令`的`-E` 、`-n`参数进行实现，`-n`选项表示只输出匹配的行，`-E`选项表示使用扩展正则表达式。`\1`表示捕获组的引用，`p`用来打印输出。

```shell
fastq=J-20230810-680-1-123808018_raw_2.fq.gz
# 提取样本编号
echo $fastq|sed -nE 's/.*([0-9]{9}).*/\1/p' 
```

### perl命令

使用`perl命令`的`-e`、`-n`、`-l`参数进行实现，`-e` 参数用于执行一行 Perl 脚本，`-n` 选项用于逐行处理输入，`-l` 选项用于自动处理行尾换行符。`$&` 表示匹配的整个字符串，`if /[0-9]+/` 表示只输出匹配数字的部分。

```shell
fastq=J-20230810-680-1-123808018_raw_2.fq.gz
# 提取样本编号
echo $fastq|perl -nle 'print $& if /[0-9]{9}/'
```

### awk命令

使用`awk命令`的`RSTART`、`RLENGTH`两个内置变量和`match`、`substr`两个函数进行实现，`match`函数用来匹配正则表达式，`substr` 函数用于返回指定字符串的子字符串，`RSTART` 匹配字符串的起始位置， `RLENGTH`匹配字符串的长度。

```shell
fastq=J-20230810-680-1-123808018_raw_2.fq.gz
# 提取样本编号
echo $fastq|awk 'match($0, /[0-9]+/) {print substr($0, RSTART, RLENGTH)}'
```

