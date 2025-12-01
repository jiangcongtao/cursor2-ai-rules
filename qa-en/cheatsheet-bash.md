# Bash Cheatsheet

## Table of Contents
- [Bash Cheatsheet](#bash-cheatsheet)
  - [Table of Contents](#table-of-contents)
  - [File Operations](#file-operations)
    - [View Files](#view-files)
    - [Create and Edit](#create-and-edit)
    - [Copy and Move](#copy-and-move)
    - [Delete](#delete)
    - [Find Files](#find-files)
  - [Directory Operations](#directory-operations)
  - [Text Processing](#text-processing)
    - [grep - Search Text](#grep---search-text)
    - [sed - Stream Editor](#sed---stream-editor)
    - [awk - Text Processing Tool](#awk---text-processing-tool)
    - [Other Text Tools](#other-text-tools)
  - [Permissions Management](#permissions-management)
  - [Process Management](#process-management)
  - [Variables and Parameters](#variables-and-parameters)
    - [Variable Operations](#variable-operations)
    - [Special Variables](#special-variables)
    - [String Operations](#string-operations)
  - [Control Structures](#control-structures)
    - [Conditional Statements](#conditional-statements)
    - [Loops](#loops)
    - [case Statement](#case-statement)
  - [Functions](#functions)
  - [Input/Output Redirection](#inputoutput-redirection)
  - [Pipes and Command Substitution](#pipes-and-command-substitution)
  - [Wildcards and Regular Expressions](#wildcards-and-regular-expressions)
    - [Wildcards (Glob)](#wildcards-glob)
    - [Regular Expressions (for grep, sed, awk)](#regular-expressions-for-grep-sed-awk)
  - [Debugging and Error Handling](#debugging-and-error-handling)
  - [Common Keyboard Shortcuts](#common-keyboard-shortcuts)
  - [Practical Tips](#practical-tips)
    - [Command Combinations](#command-combinations)
    - [Background and Foreground](#background-and-foreground)
    - [Aliases](#aliases)
    - [Command History](#command-history)
    - [Compression and Extraction](#compression-and-extraction)
    - [Network Tools](#network-tools)
    - [System Information](#system-information)
  - [Script Examples](#script-examples)
    - [Basic Script Template](#basic-script-template)
    - [Argument Parsing Example](#argument-parsing-example)
  - [Reference Resources](#reference-resources)

---

## File Operations

### View Files
```bash
cat file.txt              # Display entire file content
less file.txt             # View file page by page (scrollable)
more file.txt             # View file page by page (forward only)
head -n 10 file.txt       # Display first 10 lines
tail -n 10 file.txt       # Display last 10 lines
tail -f file.txt          # Follow file end in real-time (log monitoring)
```

### Create and Edit
```bash
touch file.txt            # Create empty file or update file timestamp
nano file.txt             # Edit with nano editor
vim file.txt              # Edit with vim editor
```

### Copy and Move
```bash
cp source.txt dest.txt    # Copy file
cp -r dir1 dir2           # Recursively copy directory
mv old.txt new.txt        # Move or rename file
```

### Delete
```bash
rm file.txt               # Delete file
rm -r dir/                # Recursively delete directory
rm -rf dir/               # Force recursive delete (dangerous!)
```

### Find Files
```bash
find . -name "*.txt"      # Find all .txt files in current directory
find . -type f -name "*.log"  # Find all .log files
find /home -user username # Find files owned by a user
locate filename           # Quick file search (requires updatedb)
which command             # Find command location
whereis command           # Find command, source, and manual page locations
```

---

## Directory Operations

```bash
pwd                       # Print current working directory
cd /path/to/dir           # Change to specified directory
cd ~                      # Change to user home directory
cd -                      # Change to previous directory
cd ..                     # Go up one directory level
ls                        # List current directory contents
ls -l                     # Detailed list (long format)
ls -a                     # Show all files (including hidden files)
ls -lh                    # Human-readable file sizes
ls -lt                    # Sort by time
mkdir dirname             # Create directory
mkdir -p path/to/dir      # Create nested directories
rmdir dirname             # Remove empty directory
tree                      # Display directory structure as tree (requires tree package)
```

---

## Text Processing

### grep - Search Text
```bash
grep "pattern" file.txt   # Search for lines containing pattern
grep -i "pattern" file.txt  # Case-insensitive search
grep -r "pattern" dir/    # Recursively search directory
grep -v "pattern" file.txt  # Show non-matching lines
grep -n "pattern" file.txt  # Show line numbers
grep -E "regex" file.txt  # Use extended regular expressions
```

### sed - Stream Editor
```bash
sed 's/old/new/g' file.txt        # Replace all old with new
sed -i 's/old/new/g' file.txt     # Modify file in place
sed '2d' file.txt                 # Delete line 2
sed '2,5d' file.txt               # Delete lines 2-5
sed '2a\new line' file.txt        # Insert after line 2
sed '/pattern/d' file.txt         # Delete lines containing pattern
```

### awk - Text Processing Tool
```bash
awk '{print $1}' file.txt         # Print first column
awk -F: '{print $1}' file.txt     # Use : as delimiter
awk '/pattern/ {print $0}' file.txt  # Print matching lines
awk '{sum+=$1} END {print sum}' file.txt  # Calculate sum of first column
```

### Other Text Tools
```bash
cut -d: -f1 file.txt      # Use : delimiter, get first field
cut -c1-10 file.txt       # Get characters 1-10
sort file.txt             # Sort
sort -r file.txt          # Reverse sort
sort -n file.txt          # Numeric sort
uniq file.txt             # Remove adjacent duplicate lines
uniq -c file.txt          # Count duplicates
wc -l file.txt            # Count lines
wc -w file.txt            # Count words
wc -c file.txt            # Count characters
```

---

## Permissions Management

```bash
chmod 755 file.txt        # Set permissions (rwxr-xr-x)
chmod +x script.sh        # Add execute permission
chmod -R 755 dir/         # Recursively set permissions
chown user:group file.txt # Change owner and group
chgrp group file.txt      # Change group

# Permission numeric notation:
# 4 = read(r), 2 = write(w), 1 = execute(x)
# 755 = rwxr-xr-x (owner rwx, group r-x, others r-x)
```

---

## Process Management

```bash
ps                        # Show current processes
ps aux                    # Show detailed info for all processes
ps -ef                    # Alternative format for all processes
top                       # Real-time process display (like task manager)
htop                      # More user-friendly top (requires installation)
kill PID                  # Terminate process
kill -9 PID               # Force terminate process
killall process_name      # Kill all processes with same name
jobs                      # Show background jobs
fg %1                     # Bring background job 1 to foreground
bg %1                     # Put job 1 in background
nohup command &          # Run in background, continue after terminal closes
```

---

## Variables and Parameters

### Variable Operations
```bash
VAR="value"               # Define variable (no spaces around =)
echo $VAR                 # Output variable value
echo ${VAR}               # Safer variable reference
unset VAR                 # Delete variable
readonly VAR="value"      # Define read-only variable
export VAR="value"        # Export as environment variable
```

### Special Variables
```bash
$0                        # Script name
$1, $2, ...               # Positional parameters
$#                        # Number of arguments
$@                        # All arguments (as separate strings)
$*                        # All arguments (as single string)
$?                        # Exit status of last command
$$                        # Current process ID
$!                        # Last background process ID
```

### String Operations
```bash
${VAR:-default}           # Use default if VAR is empty
${VAR:=default}           # Set and use default if VAR is empty
${VAR:+value}             # Use value if VAR is not empty
${VAR:offset}             # Substring from offset
${VAR:offset:length}      # Substring from offset with length
${#VAR}                   # String length
${VAR#pattern}            # Remove shortest matching prefix
${VAR##pattern}           # Remove longest matching prefix
${VAR%pattern}            # Remove shortest matching suffix
${VAR%%pattern}           # Remove longest matching suffix
${VAR/old/new}            # Replace first match
${VAR//old/new}           # Replace all matches
```

---

## Control Structures

### Conditional Statements
```bash
# if-else
if [ condition ]; then
    commands
elif [ condition ]; then
    commands
else
    commands
fi

# Condition test operators
[ -f file ]               # File exists and is regular file
[ -d dir ]                # Directory exists
[ -e path ]               # Path exists
[ -r file ]               # File is readable
[ -w file ]               # File is writable
[ -x file ]               # File is executable
[ -z string ]             # String is empty
[ -n string ]             # String is not empty
[ str1 = str2 ]           # Strings are equal
[ str1 != str2 ]          # Strings are not equal
[ num1 -eq num2 ]         # Numbers are equal
[ num1 -ne num2 ]         # Numbers are not equal
[ num1 -lt num2 ]         # num1 < num2
[ num1 -le num2 ]         # num1 <= num2
[ num1 -gt num2 ]         # num1 > num2
[ num1 -ge num2 ]         # num1 >= num2
[ ! condition ]           # Logical NOT
[ cond1 ] && [ cond2 ]    # Logical AND
[ cond1 ] || [ cond2 ]    # Logical OR
```

### Loops
```bash
# for loop
for var in list; do
    commands
done

# C-style for loop
for ((i=0; i<10; i++)); do
    commands
done

# while loop
while [ condition ]; do
    commands
done

# until loop
until [ condition ]; do
    commands
done

# Iterate over files
for file in *.txt; do
    echo "$file"
done
```

### case Statement
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

## Functions

```bash
# Define function
function_name() {
    commands
    return value
}

# Or use function keyword
function function_name {
    commands
}

# Call function
function_name arg1 arg2

# Function parameters
# $1, $2, ... represent function arguments
# $# represents number of arguments
```

---

## Input/Output Redirection

```bash
command > file            # Redirect stdout to file (overwrite)
command >> file           # Append stdout to file
command < file            # Read stdin from file
command 2> file           # Redirect stderr to file
command 2>> file          # Append stderr to file
command > file 2>&1       # Redirect both stdout and stderr to file
command &> file           # Same as above (bash 4+)
command > file1 2> file2  # Stdout to file1, stderr to file2
command << EOF            # Here document
    text
EOF
```

---

## Pipes and Command Substitution

```bash
# Pipe
command1 | command2       # Use command1 output as command2 input

# Command substitution
$(command)                # Execute command and substitute with output
`command`                 # Old-style command substitution (not recommended)

# Examples
echo "Today is $(date)"
files=$(ls)
```

---

## Wildcards and Regular Expressions

### Wildcards (Glob)
```bash
*                         # Match any characters (0 or more)
?                         # Match single character
[abc]                     # Match a, b, or c
[a-z]                     # Match any character from a to z
[!abc]                    # Don't match a, b, c
{1,2,3}                   # Match 1, 2, or 3
{1..10}                   # Match 1 through 10
```

### Regular Expressions (for grep, sed, awk)
```bash
.                         # Match any single character
^                         # Start of line
$                         # End of line
*                         # Previous character 0 or more times
+                         # Previous character 1 or more times (requires -E)
?                         # Previous character 0 or 1 time (requires -E)
{n}                       # Previous character n times
{n,m}                     # Previous character n to m times
[abc]                     # Character class
[^abc]                    # Negated character class
|                         # OR (requires -E)
()                        # Grouping (requires -E)
\                         # Escape character
```

---

## Debugging and Error Handling

```bash
#!/bin/bash
set -e                     # Exit immediately on error
set -u                     # Error on undefined variables
set -x                     # Display executed commands
set -o pipefail            # Return failure if any command in pipeline fails

# Error handling example
command || {
    echo "Error occurred"
    exit 1
}

# trap to catch signals
trap 'echo "Script interrupted"; exit' INT TERM
```

---

## Common Keyboard Shortcuts

```bash
Ctrl+C                    # Interrupt current command
Ctrl+D                    # Exit shell (EOF)
Ctrl+L                    # Clear screen (same as clear)
Ctrl+A                    # Move to beginning of line
Ctrl+E                    # Move to end of line
Ctrl+U                    # Delete everything before cursor
Ctrl+K                    # Delete everything after cursor
Ctrl+W                    # Delete word before cursor
Ctrl+Y                    # Paste previously deleted content
Ctrl+R                    # Search command history
Ctrl+Z                    # Suspend process (can resume with fg)
!!                        # Execute previous command
!$                        # Last argument of previous command
!n                        # Execute command n from history
```

---

## Practical Tips

### Command Combinations
```bash
command1 && command2      # Execute command2 only if command1 succeeds
command1 || command2      # Execute command2 only if command1 fails
command1 ; command2       # Execute sequentially (regardless of success/failure)
```

### Background and Foreground
```bash
command &                 # Run in background
command1 && command2 &   # Run combined commands in background
```

### Aliases
```bash
alias ll='ls -lh'         # Create alias
alias grep='grep --color=auto'  # Colored grep
unalias ll                # Remove alias
```

### Command History
```bash
history                   # Show command history
history | grep "pattern"  # Search command history
!n                        # Execute command n from history
!!                        # Execute previous command
```

### Compression and Extraction
```bash
tar -czf archive.tar.gz dir/    # Create gzip archive
tar -xzf archive.tar.gz          # Extract gzip archive
tar -cjf archive.tar.bz2 dir/    # Create bzip2 archive
tar -xjf archive.tar.bz2         # Extract bzip2 archive
zip -r archive.zip dir/          # Create zip archive
unzip archive.zip                # Extract zip archive
```

### Network Tools
```bash
ping hostname              # Test network connectivity
curl URL                   # Download URL content
wget URL                   # Download file
ssh user@host             # SSH connection
scp file user@host:/path  # Secure copy file
```

### System Information
```bash
uname -a                  # System information
df -h                     # Disk usage
du -h dir/                # Directory size
free -h                   # Memory usage
uptime                    # System uptime
whoami                    # Current username
id                        # User ID and group ID
```

---

## Script Examples

### Basic Script Template
```bash
#!/bin/bash
# Script description

set -euo pipefail          # Strict mode

# Variable definitions
SCRIPT_DIR="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"
LOG_FILE="${SCRIPT_DIR}/script.log"

# Function definitions
log() {
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] $*" | tee -a "$LOG_FILE"
}

# Main logic
main() {
    log "Script started"
    # Your code here
    log "Script completed"
}

# Execute main function
main "$@"
```

### Argument Parsing Example
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

## Reference Resources

- [Bash Manual](https://www.gnu.org/software/bash/manual/)
- [Bash Guide for Beginners](https://tldp.org/LDP/Bash-Beginners-Guide/html/)
- [Advanced Bash Scripting Guide](https://tldp.org/LDP/abs/html/)

---

_ Disclaimer: This content is AI-generated. Please verify all facts and details prior to use. _

--- By Cursor AI

