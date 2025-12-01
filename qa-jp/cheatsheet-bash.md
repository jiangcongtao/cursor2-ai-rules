# Bash チートシート (Bash Cheatsheet)

## 目次
- [ファイル操作](#ファイル操作)
- [ディレクトリ操作](#ディレクトリ操作)
- [テキスト処理](#テキスト処理)
- [権限管理](#権限管理)
- [プロセス管理](#プロセス管理)
- [変数とパラメータ](#変数とパラメータ)
- [制御構造](#制御構造)
- [関数](#関数)
- [入出力リダイレクト](#入出力リダイレクト)
- [パイプとコマンド置換](#パイプとコマンド置換)
- [ワイルドカードと正規表現](#ワイルドカードと正規表現)
- [デバッグとエラー処理](#デバッグとエラー処理)
- [よく使うショートカット](#よく使うショートカット)

---

## ファイル操作

### ファイルの閲覧
```bash
cat file.txt              # ファイル全体を表示
less file.txt             # ページ単位で閲覧（上下スクロール可能）
more file.txt             # ページ単位で閲覧（下方向のみ）
head -n 10 file.txt       # 最初の10行を表示
tail -n 10 file.txt       # 最後の10行を表示
tail -f file.txt          # ファイル末尾をリアルタイムで追跡（ログ監視）
```

### 作成と編集
```bash
touch file.txt            # 空ファイルを作成またはタイムスタンプを更新
nano file.txt             # nanoエディタを使用
vim file.txt              # vimエディタを使用
```

### コピーと移動
```bash
cp source.txt dest.txt    # ファイルをコピー
cp -r dir1 dir2           # ディレクトリを再帰的にコピー
mv old.txt new.txt        # ファイルを移動またはリネーム
```

### 削除
```bash
rm file.txt               # ファイルを削除
rm -r dir/                # ディレクトリを再帰的に削除
rm -rf dir/               # 強制的に再帰的に削除（危険！）
```

### ファイル検索
```bash
find . -name "*.txt"      # 現在のディレクトリ下のすべての.txtファイルを検索
find . -type f -name "*.log"  # すべての.logファイルを検索
find /home -user username # 特定ユーザーのファイルを検索
locate filename           # ファイルを高速検索（updatedbが必要）
which command             # コマンドの場所を検索
whereis command           # コマンド、ソース、マニュアルページの場所を検索
```

---

## ディレクトリ操作

```bash
pwd                       # 現在の作業ディレクトリを表示
cd /path/to/dir           # 指定ディレクトリに移動
cd ~                      # ユーザーのホームディレクトリに移動
cd -                      # 前のディレクトリに移動
cd ..                     # 親ディレクトリに戻る
ls                        # 現在のディレクトリの内容を一覧表示
ls -l                     # 詳細リスト（長い形式）
ls -a                     # すべてのファイルを表示（隠しファイル含む）
ls -lh                    # 人間が読みやすいファイルサイズ
ls -lt                    # 時間順にソート
mkdir dirname             # ディレクトリを作成
mkdir -p path/to/dir      # 複数階層のディレクトリを作成
rmdir dirname             # 空のディレクトリを削除
tree                      # ディレクトリ構造をツリー表示（treeのインストールが必要）
```

---

## テキスト処理

### grep - テキスト検索
```bash
grep "pattern" file.txt   # patternを含む行を検索
grep -i "pattern" file.txt  # 大文字小文字を区別しない
grep -r "pattern" dir/    # ディレクトリを再帰的に検索
grep -v "pattern" file.txt  # 一致しない行を表示
grep -n "pattern" file.txt  # 行番号を表示
grep -E "regex" file.txt  # 拡張正規表現を使用
```

### sed - ストリームエディタ
```bash
sed 's/old/new/g' file.txt        # すべてのoldをnewに置換
sed -i 's/old/new/g' file.txt     # ファイルを直接編集
sed '2d' file.txt                 # 2行目を削除
sed '2,5d' file.txt               # 2-5行を削除
sed '2a\new line' file.txt        # 2行目の後に挿入
sed '/pattern/d' file.txt         # patternを含む行を削除
```

### awk - テキスト処理ツール
```bash
awk '{print $1}' file.txt         # 1列目を表示
awk -F: '{print $1}' file.txt     # :を区切り文字として使用
awk '/pattern/ {print $0}' file.txt  # 一致する行を表示
awk '{sum+=$1} END {print sum}' file.txt  # 1列目の合計を計算
```

### その他のテキストツール
```bash
cut -d: -f1 file.txt      # :で区切り、1番目のフィールドを取得
cut -c1-10 file.txt       # 1-10文字目を取得
sort file.txt             # ソート
sort -r file.txt          # 逆順ソート
sort -n file.txt          # 数値ソート
uniq file.txt             # 隣接する重複行を削除
uniq -c file.txt          # 重複回数をカウント
wc -l file.txt            # 行数をカウント
wc -w file.txt            # 単語数をカウント
wc -c file.txt            # 文字数をカウント
```

---

## 権限管理

```bash
chmod 755 file.txt        # 権限を設定（rwxr-xr-x）
chmod +x script.sh        # 実行権限を追加
chmod -R 755 dir/         # 再帰的に権限を設定
chown user:group file.txt # 所有者とグループを変更
chgrp group file.txt      # グループを変更

# 権限の数値表現：
# 4 = 読む(r), 2 = 書く(w), 1 = 実行(x)
# 755 = rwxr-xr-x (所有者rwx、グループr-x、その他r-x)
```

---

## プロセス管理

```bash
ps                        # 現在のプロセスを表示
ps aux                    # すべてのプロセスの詳細情報を表示
ps -ef                    # すべてのプロセスを別形式で表示
top                       # プロセスをリアルタイム表示（タスクマネージャー類似）
htop                      # より使いやすいtop（インストールが必要）
kill PID                  # プロセスを終了
kill -9 PID               # プロセスを強制終了
killall process_name      # 同名のすべてのプロセスを終了
jobs                      # バックグラウンドタスクを表示
fg %1                     # バックグラウンドタスク1をフォアグラウンドに
bg %1                     # タスク1をバックグラウンドで実行
nohup command &          # バックグラウンドで実行、ターミナル終了後も継続
```

---

## 変数とパラメータ

### 変数操作
```bash
VAR="value"               # 変数を定義（等号の両側にスペースを入れない）
echo $VAR                 # 変数の値を出力
echo ${VAR}               # より安全な変数参照方法
unset VAR                 # 変数を削除
readonly VAR="value"      # 読み取り専用変数を定義
export VAR="value"        # 環境変数としてエクスポート
```

### 特殊変数
```bash
$0                        # スクリプト名
$1, $2, ...               # 位置パラメータ
$#                        # パラメータの数
$@                        # すべてのパラメータ（個別の文字列として）
$*                        # すべてのパラメータ（単一の文字列として）
$?                        # 前のコマンドの終了ステータス
$$                        # 現在のプロセスID
$!                        # 最後のバックグラウンドプロセスのID
```

### 文字列操作
```bash
${VAR:-default}           # VARが空の場合、defaultを使用
${VAR:=default}           # VARが空の場合、defaultを設定して使用
${VAR:+value}             # VARが空でない場合、valueを使用
${VAR:offset}             # offsetから切り取り
${VAR:offset:length}      # offsetからlengthの長さで切り取り
${#VAR}                   # 文字列の長さ
${VAR#pattern}            # 最短一致のプレフィックスを削除
${VAR##pattern}           # 最長一致のプレフィックスを削除
${VAR%pattern}            # 最短一致のサフィックスを削除
${VAR%%pattern}           # 最長一致のサフィックスを削除
${VAR/old/new}            # 最初の一致を置換
${VAR//old/new}           # すべての一致を置換
```

---

## 制御構造

### 条件分岐
```bash
# if-else
if [ condition ]; then
    commands
elif [ condition ]; then
    commands
else
    commands
fi

# 条件テスト演算子
[ -f file ]               # ファイルが存在し、通常ファイルである
[ -d dir ]                # ディレクトリが存在する
[ -e path ]               # パスが存在する
[ -r file ]               # ファイルが読み取り可能
[ -w file ]               # ファイルが書き込み可能
[ -x file ]               # ファイルが実行可能
[ -z string ]             # 文字列が空
[ -n string ]             # 文字列が空でない
[ str1 = str2 ]           # 文字列が等しい
[ str1 != str2 ]          # 文字列が等しくない
[ num1 -eq num2 ]         # 数値が等しい
[ num1 -ne num2 ]         # 数値が等しくない
[ num1 -lt num2 ]         # num1 < num2
[ num1 -le num2 ]         # num1 <= num2
[ num1 -gt num2 ]         # num1 > num2
[ num1 -ge num2 ]         # num1 >= num2
[ ! condition ]           # 論理否定
[ cond1 ] && [ cond2 ]    # 論理AND
[ cond1 ] || [ cond2 ]    # 論理OR
```

### ループ
```bash
# forループ
for var in list; do
    commands
done

# Cスタイルのforループ
for ((i=0; i<10; i++)); do
    commands
done

# whileループ
while [ condition ]; do
    commands
done

# untilループ
until [ condition ]; do
    commands
done

# ファイルの走査
for file in *.txt; do
    echo "$file"
done
```

### case文
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

## 関数

```bash
# 関数の定義
function_name() {
    commands
    return value
}

# またはfunctionキーワードを使用
function function_name {
    commands
}

# 関数の呼び出し
function_name arg1 arg2

# 関数のパラメータ
# $1, $2, ... は関数のパラメータを表す
# $# はパラメータの数を表す
```

---

## 入出力リダイレクト

```bash
command > file            # 標準出力をファイルにリダイレクト（上書き）
command >> file           # 標準出力をファイルに追加
command < file            # ファイルから標準入力を読み取る
command 2> file           # 標準エラーをファイルにリダイレクト
command 2>> file          # 標準エラーをファイルに追加
command > file 2>&1       # 標準出力とエラーを両方ファイルにリダイレクト
command &> file           # 同上（bash 4+）
command > file1 2> file2  # 標準出力をfile1に、エラーをfile2に
command << EOF            # Hereドキュメント
    text
EOF
```

---

## パイプとコマンド置換

```bash
# パイプ
command1 | command2       # command1の出力をcommand2の入力にする

# コマンド置換
$(command)                # コマンドを実行し、出力で置換
`command`                 # 古い形式のコマンド置換（非推奨）

# 例
echo "Today is $(date)"
files=$(ls)
```

---

## ワイルドカードと正規表現

### ワイルドカード（Glob）
```bash
*                         # 任意の文字に一致（0個以上）
?                         # 単一の文字に一致
[abc]                     # a、b、またはcに一致
[a-z]                     # aからzの任意の文字に一致
[!abc]                    # a、b、c以外に一致
{1,2,3}                   # 1、2、または3に一致
{1..10}                   # 1から10に一致
```

### 正規表現（grep、sed、awkで使用）
```bash
.                         # 任意の単一文字に一致
^                         # 行の先頭
$                         # 行の末尾
*                         # 前の文字が0回以上
+                         # 前の文字が1回以上（-Eが必要）
?                         # 前の文字が0回または1回（-Eが必要）
{n}                       # 前の文字がn回
{n,m}                     # 前の文字がn回からm回
[abc]                     # 文字クラス
[^abc]                    # 否定文字クラス
|                         # または（-Eが必要）
()                        # グループ化（-Eが必要）
\                         # エスケープ文字
```

---

## デバッグとエラー処理

```bash
#!/bin/bash
set -e                     # エラーが発生したら即座に終了
set -u                     # 未定義変数を使用した場合にエラー
set -x                     # 実行するコマンドを表示
set -o pipefail            # パイプ内のいずれかのコマンドが失敗した場合に失敗を返す

# エラー処理の例
command || {
    echo "Error occurred"
    exit 1
}

# trapでシグナルをキャッチ
trap 'echo "Script interrupted"; exit' INT TERM
```

---

## よく使うショートカット

```bash
Ctrl+C                    # 現在のコマンドを中断
Ctrl+D                    # shellを終了（EOF）
Ctrl+L                    # 画面をクリア（clearと同じ）
Ctrl+A                    # 行の先頭に移動
Ctrl+E                    # 行の末尾に移動
Ctrl+U                    # カーソル前のすべてを削除
Ctrl+K                    # カーソル後のすべてを削除
Ctrl+W                    # カーソル前の単語を削除
Ctrl+Y                    # 削除した内容を貼り付け
Ctrl+R                    # コマンド履歴を検索
Ctrl+Z                    # プロセスを一時停止（fgで復帰可能）
!!                        # 前のコマンドを実行
!$                        # 前のコマンドの最後のパラメータ
!n                        # 履歴のn番目のコマンドを実行
```

---

## 実用的なテクニック

### コマンドの組み合わせ
```bash
command1 && command2      # command1が成功した場合のみcommand2を実行
command1 || command2      # command1が失敗した場合のみcommand2を実行
command1 ; command2       # 順次実行（成功失敗に関係なく）
```

### バックグラウンドとフォアグラウンド
```bash
command &                 # バックグラウンドで実行
command1 && command2 &    # 組み合わせコマンドをバックグラウンドで実行
```

### エイリアス
```bash
alias ll='ls -lh'         # エイリアスを作成
alias grep='grep --color=auto'  # 色付きのgrep
unalias ll                # エイリアスを削除
```

### コマンド履歴
```bash
history                   # コマンド履歴を表示
history | grep "pattern"  # コマンド履歴を検索
!n                        # 履歴のn番目のコマンドを実行
!!                        # 前のコマンドを実行
```

### 圧縮と解凍
```bash
tar -czf archive.tar.gz dir/    # gzipアーカイブを作成
tar -xzf archive.tar.gz          # gzipアーカイブを解凍
tar -cjf archive.tar.bz2 dir/    # bzip2アーカイブを作成
tar -xjf archive.tar.bz2         # bzip2アーカイブを解凍
zip -r archive.zip dir/          # zipアーカイブを作成
unzip archive.zip                # zipアーカイブを解凍
```

### ネットワークツール
```bash
ping hostname              # ネットワーク接続をテスト
curl URL                   # URLの内容をダウンロード
wget URL                   # ファイルをダウンロード
ssh user@host             # SSH接続
scp file user@host:/path  # ファイルを安全にコピー
```

### システム情報
```bash
uname -a                  # システム情報
df -h                     # ディスク使用状況
du -h dir/                # ディレクトリサイズ
free -h                   # メモリ使用状況
uptime                    # システム稼働時間
whoami                    # 現在のユーザー名
id                        # ユーザーIDとグループID
```

---

## スクリプト例

### 基本的なスクリプトテンプレート
```bash
#!/bin/bash
# スクリプトの説明

set -euo pipefail          # 厳密モード

# 変数定義
SCRIPT_DIR="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"
LOG_FILE="${SCRIPT_DIR}/script.log"

# 関数定義
log() {
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] $*" | tee -a "$LOG_FILE"
}

# メインロジック
main() {
    log "Script started"
    # あなたのコード
    log "Script completed"
}

# メイン関数を実行
main "$@"
```

### パラメータ解析の例
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

## 参考リソース

- [Bash Manual](https://www.gnu.org/software/bash/manual/)
- [Bash Guide for Beginners](https://tldp.org/LDP/Bash-Beginners-Guide/html/)
- [Advanced Bash Scripting Guide](https://tldp.org/LDP/abs/html/)

---

_ Disclaimer: This content is AI-generated. Please verify all facts and details prior to use. _

--- By Cursor AI

