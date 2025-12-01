# Bash 速查表 (Bash Cheatsheet)

## 目录
- [文件操作](#文件操作)
- [目录操作](#目录操作)
- [文本处理](#文本处理)
- [权限管理](#权限管理)
- [进程管理](#进程管理)
- [变量和参数](#变量和参数)
- [控制结构](#控制结构)
- [函数](#函数)
- [输入输出重定向](#输入输出重定向)
- [管道和命令替换](#管道和命令替换)
- [通配符和正则表达式](#通配符和正则表达式)
- [调试和错误处理](#调试和错误处理)
- [常用快捷键](#常用快捷键)

---

## 文件操作

### 查看文件
```bash
cat file.txt              # 显示整个文件内容
less file.txt             # 分页查看文件（可上下滚动）
more file.txt             # 分页查看文件（只能向下）
head -n 10 file.txt       # 显示前10行
tail -n 10 file.txt       # 显示后10行
tail -f file.txt          # 实时跟踪文件末尾（日志监控）
```

### 创建和编辑
```bash
touch file.txt            # 创建空文件或更新文件时间戳
nano file.txt             # 使用nano编辑器
vim file.txt              # 使用vim编辑器
```

### 复制和移动
```bash
cp source.txt dest.txt    # 复制文件
cp -r dir1 dir2           # 递归复制目录
mv old.txt new.txt        # 移动或重命名文件
```

### 删除
```bash
rm file.txt               # 删除文件
rm -r dir/                # 递归删除目录
rm -rf dir/               # 强制递归删除（危险！）
```

### 查找文件
```bash
find . -name "*.txt"      # 查找当前目录下所有.txt文件
find . -type f -name "*.log"  # 查找所有.log文件
find /home -user username # 查找属于某用户的文件
locate filename           # 快速查找文件（需要updatedb）
which command             # 查找命令的位置
whereis command           # 查找命令、源码和手册页位置
```

---

## 目录操作

```bash
pwd                       # 显示当前工作目录
cd /path/to/dir           # 切换到指定目录
cd ~                      # 切换到用户主目录
cd -                      # 切换到上一个目录
cd ..                     # 返回上一级目录
ls                        # 列出当前目录内容
ls -l                     # 详细列表（长格式）
ls -a                     # 显示所有文件（包括隐藏文件）
ls -lh                    # 人类可读的文件大小
ls -lt                    # 按时间排序
mkdir dirname             # 创建目录
mkdir -p path/to/dir      # 创建多级目录
rmdir dirname             # 删除空目录
tree                      # 树形显示目录结构（需要安装tree）
```

---

## 文本处理

### grep - 搜索文本
```bash
grep "pattern" file.txt   # 搜索包含pattern的行
grep -i "pattern" file.txt  # 忽略大小写
grep -r "pattern" dir/    # 递归搜索目录
grep -v "pattern" file.txt  # 显示不匹配的行
grep -n "pattern" file.txt  # 显示行号
grep -E "regex" file.txt  # 使用扩展正则表达式
```

### sed - 流编辑器
```bash
sed 's/old/new/g' file.txt        # 替换所有old为new
sed -i 's/old/new/g' file.txt     # 原地修改文件
sed '2d' file.txt                 # 删除第2行
sed '2,5d' file.txt               # 删除2-5行
sed '2a\new line' file.txt        # 在第2行后插入
sed '/pattern/d' file.txt         # 删除包含pattern的行
```

### awk - 文本处理工具
```bash
awk '{print $1}' file.txt         # 打印第1列
awk -F: '{print $1}' file.txt     # 使用:作为分隔符
awk '/pattern/ {print $0}' file.txt  # 打印匹配的行
awk '{sum+=$1} END {print sum}' file.txt  # 计算第1列总和
```

### 其他文本工具
```bash
cut -d: -f1 file.txt      # 使用:分隔，取第1字段
cut -c1-10 file.txt       # 取第1-10个字符
sort file.txt             # 排序
sort -r file.txt          # 逆序排序
sort -n file.txt          # 数字排序
uniq file.txt             # 去除相邻重复行
uniq -c file.txt          # 统计重复次数
wc -l file.txt            # 统计行数
wc -w file.txt            # 统计单词数
wc -c file.txt            # 统计字符数
```

---

## 权限管理

```bash
chmod 755 file.txt        # 设置权限（rwxr-xr-x）
chmod +x script.sh        # 添加执行权限
chmod -R 755 dir/         # 递归设置权限
chown user:group file.txt # 更改所有者和组
chgrp group file.txt      # 更改组

# 权限数字表示：
# 4 = 读(r), 2 = 写(w), 1 = 执行(x)
# 755 = rwxr-xr-x (所有者rwx，组r-x，其他r-x)
```

---

## 进程管理

```bash
ps                        # 显示当前进程
ps aux                    # 显示所有进程的详细信息
ps -ef                    # 另一种格式显示所有进程
top                       # 实时显示进程（类似任务管理器）
htop                      # 更友好的top（需要安装）
kill PID                  # 终止进程
kill -9 PID               # 强制终止进程
killall process_name      # 终止所有同名进程
jobs                      # 显示后台任务
fg %1                     # 将后台任务1调到前台
bg %1                     # 将任务1放到后台运行
nohup command &          # 后台运行，终端关闭后继续
```

---

## 变量和参数

### 变量操作
```bash
VAR="value"               # 定义变量（注意等号两边不能有空格）
echo $VAR                 # 输出变量值
echo ${VAR}               # 更安全的变量引用方式
unset VAR                 # 删除变量
readonly VAR="value"      # 定义只读变量
export VAR="value"        # 导出为环境变量
```

### 特殊变量
```bash
$0                        # 脚本名称
$1, $2, ...               # 位置参数
$#                        # 参数个数
$@                        # 所有参数（作为独立字符串）
$*                        # 所有参数（作为单个字符串）
$?                        # 上一个命令的退出状态
$$                        # 当前进程ID
$!                        # 最后一个后台进程ID
```

### 字符串操作
```bash
${VAR:-default}           # 如果VAR为空，使用default
${VAR:=default}           # 如果VAR为空，设置并使用default
${VAR:+value}             # 如果VAR不为空，使用value
${VAR:offset}             # 从offset开始截取
${VAR:offset:length}      # 从offset开始截取length长度
${#VAR}                   # 字符串长度
${VAR#pattern}            # 删除最短匹配前缀
${VAR##pattern}           # 删除最长匹配前缀
${VAR%pattern}            # 删除最短匹配后缀
${VAR%%pattern}           # 删除最长匹配后缀
${VAR/old/new}            # 替换第一个匹配
${VAR//old/new}           # 替换所有匹配
```

---

## 控制结构

### 条件判断
```bash
# if-else
if [ condition ]; then
    commands
elif [ condition ]; then
    commands
else
    commands
fi

# 条件测试操作符
[ -f file ]               # 文件存在且为普通文件
[ -d dir ]                # 目录存在
[ -e path ]               # 路径存在
[ -r file ]               # 文件可读
[ -w file ]               # 文件可写
[ -x file ]               # 文件可执行
[ -z string ]             # 字符串为空
[ -n string ]             # 字符串非空
[ str1 = str2 ]           # 字符串相等
[ str1 != str2 ]          # 字符串不等
[ num1 -eq num2 ]         # 数字相等
[ num1 -ne num2 ]         # 数字不等
[ num1 -lt num2 ]         # num1 < num2
[ num1 -le num2 ]         # num1 <= num2
[ num1 -gt num2 ]         # num1 > num2
[ num1 -ge num2 ]         # num1 >= num2
[ ! condition ]           # 逻辑非
[ cond1 ] && [ cond2 ]    # 逻辑与
[ cond1 ] || [ cond2 ]    # 逻辑或
```

### 循环
```bash
# for循环
for var in list; do
    commands
done

# C风格for循环
for ((i=0; i<10; i++)); do
    commands
done

# while循环
while [ condition ]; do
    commands
done

# until循环
until [ condition ]; do
    commands
done

# 遍历文件
for file in *.txt; do
    echo "$file"
done
```

### case语句
```bash
case $var in
    pattern1)
        commands
        ;;
    pattern2)
        commands
        ;;
    *)
        commands
        ;;
esac
```

---

## 函数

```bash
# 定义函数
function_name() {
    commands
    return value
}

# 或使用function关键字
function function_name {
    commands
}

# 调用函数
function_name arg1 arg2

# 函数参数
# $1, $2, ... 表示函数参数
# $# 表示参数个数
```

---

## 输入输出重定向

```bash
command > file            # 标准输出重定向到文件（覆盖）
command >> file           # 标准输出追加到文件
command < file            # 从文件读取标准输入
command 2> file           # 标准错误重定向到文件
command 2>> file          # 标准错误追加到文件
command > file 2>&1       # 标准输出和错误都重定向到文件
command &> file           # 同上（bash 4+）
command > file1 2> file2  # 标准输出到file1，错误到file2
command << EOF            # Here文档
    text
EOF
```

---

## 管道和命令替换

```bash
# 管道
command1 | command2       # 将command1的输出作为command2的输入

# 命令替换
$(command)                # 执行命令并替换为输出
`command`                 # 旧式命令替换（不推荐）

# 示例
echo "Today is $(date)"
files=$(ls)
```

---

## 通配符和正则表达式

### 通配符（Glob）
```bash
*                         # 匹配任意字符（0个或多个）
?                         # 匹配单个字符
[abc]                     # 匹配a、b或c
[a-z]                     # 匹配a到z的任意字符
[!abc]                    # 不匹配a、b、c
{1,2,3}                   # 匹配1、2或3
{1..10}                   # 匹配1到10
```

### 正则表达式（用于grep、sed、awk）
```bash
.                         # 匹配任意单个字符
^                         # 行首
$                         # 行尾
*                         # 前一个字符0次或多次
+                         # 前一个字符1次或多次（需要-E）
?                         # 前一个字符0次或1次（需要-E）
{n}                       # 前一个字符n次
{n,m}                     # 前一个字符n到m次
[abc]                     # 字符类
[^abc]                    # 否定字符类
|                         # 或（需要-E）
()                        # 分组（需要-E）
\                         # 转义字符
```

---

## 调试和错误处理

```bash
#!/bin/bash
set -e                     # 遇到错误立即退出
set -u                     # 使用未定义变量时报错
set -x                     # 显示执行的命令
set -o pipefail            # 管道中任何命令失败都返回失败

# 错误处理示例
command || {
    echo "Error occurred"
    exit 1
}

# trap捕获信号
trap 'echo "Script interrupted"; exit' INT TERM
```

---

## 常用快捷键

```bash
Ctrl+C                    # 中断当前命令
Ctrl+D                    # 退出shell（EOF）
Ctrl+L                    # 清屏（等同于clear）
Ctrl+A                    # 移动到行首
Ctrl+E                    # 移动到行尾
Ctrl+U                    # 删除光标前所有内容
Ctrl+K                    # 删除光标后所有内容
Ctrl+W                    # 删除光标前一个单词
Ctrl+Y                    # 粘贴刚才删除的内容
Ctrl+R                    # 搜索命令历史
Ctrl+Z                    # 暂停进程（可用fg恢复）
!!                        # 执行上一个命令
!$                        # 上一个命令的最后一个参数
!n                        # 执行历史中第n个命令
```

---

## 实用技巧

### 组合命令
```bash
command1 && command2      # command1成功才执行command2
command1 || command2      # command1失败才执行command2
command1 ; command2       # 顺序执行（不管成功失败）
```

### 后台和前台
```bash
command &                 # 后台运行
command1 && command2 &    # 组合命令后台运行
```

### 别名
```bash
alias ll='ls -lh'         # 创建别名
alias grep='grep --color=auto'  # 带颜色的grep
unalias ll                # 删除别名
```

### 历史命令
```bash
history                   # 显示命令历史
history | grep "pattern"  # 搜索历史命令
!n                        # 执行历史中第n个命令
!!                        # 执行上一个命令
```

### 压缩和解压
```bash
tar -czf archive.tar.gz dir/    # 创建gzip压缩包
tar -xzf archive.tar.gz          # 解压gzip压缩包
tar -cjf archive.tar.bz2 dir/    # 创建bzip2压缩包
tar -xjf archive.tar.bz2         # 解压bzip2压缩包
zip -r archive.zip dir/          # 创建zip压缩包
unzip archive.zip                # 解压zip压缩包
```

### 网络工具
```bash
ping hostname              # 测试网络连接
curl URL                   # 下载URL内容
wget URL                   # 下载文件
ssh user@host             # SSH连接
scp file user@host:/path  # 安全复制文件
```

### 系统信息
```bash
uname -a                  # 系统信息
df -h                     # 磁盘使用情况
du -h dir/                # 目录大小
free -h                   # 内存使用情况
uptime                    # 系统运行时间
whoami                    # 当前用户名
id                        # 用户ID和组ID
```

---

## 脚本示例

### 基本脚本模板
```bash
#!/bin/bash
# 脚本描述

set -euo pipefail          # 严格模式

# 变量定义
SCRIPT_DIR="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"
LOG_FILE="${SCRIPT_DIR}/script.log"

# 函数定义
log() {
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] $*" | tee -a "$LOG_FILE"
}

# 主逻辑
main() {
    log "Script started"
    # 你的代码
    log "Script completed"
}

# 执行主函数
main "$@"
```

### 参数解析示例
```bash
#!/bin/bash

while [[ $# -gt 0 ]]; do
    case $1 in
        -h|--help)
            echo "Usage: $0 [OPTIONS]"
            exit 0
            ;;
        -v|--verbose)
            VERBOSE=true
            shift
            ;;
        -f|--file)
            FILE="$2"
            shift 2
            ;;
        *)
            echo "Unknown option: $1"
            exit 1
            ;;
    esac
done
```

---

## 参考资源

- [Bash Manual](https://www.gnu.org/software/bash/manual/)
- [Bash Guide for Beginners](https://tldp.org/LDP/Bash-Beginners-Guide/html/)
- [Advanced Bash Scripting Guide](https://tldp.org/LDP/abs/html/)

---

_ Disclaimer: This content is AI-generated. Please verify all facts and details prior to use. _

--- By Cursor AI

