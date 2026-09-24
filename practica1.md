1
```bash
localhost:~# grep -o '^[^:]*' /etc/passwd | sort
```
2
```bash
localhost:~# grep -v '^#' /etc/protocols | awk 'NF >= 2 {print $2, $1}' | sort -nr | head -5
```
3
```bash
#!/bin/sh
text="$1"
len=${#text}
printf '+'
printf '%*s' $((len + 2)) '' | tr ' ' '-'
printf '+\n'
printf '| %s |\n' "$text"
printf '+'
printf '%*s' $((len + 2)) '' | tr ' ' '-'
printf '+\n'
```
```bash
localhost:~# chmod +x banner
localhost:~# ./banner "Hello from RTU MIREA!"
+-----------------------+
| Hello from RTU MIREA! |
+-----------------------+
localhost:~# ./banner "hi"
+----+
| hi |
+----+
```
4
```bash
#! /bin/sh
grep -oE '[A-Za-z_][A-Za-z0-9_]*' "$1" | sort -u
```
```bash
localhost:~# chmod +x identifiers
localhost:~# ./identifiers hello.c
h
hello
include
int
main
n
printf
return
stdio
void
world
```
5
```bash
#!/bin/sh
chmod +x "$1"
cp "$1" /usr/local/bin/
```
```
localhost:~# chmod +x reg
localhost:~# ./reg banner
localhost:~# ./banner "Hello"
+-------+
| Hello |
+-------+
```
6
```bash
#!/bin/sh
case "$1" in
        *.c|*.js)
        head -1 "$1" | grep '^//'
        ;;
        *.py)
        head -1 "$1" | grep '^#'
        ;;
esac
```
```bash
localhost:~# chmod +x check_comments
localhost:~# ./check_comments hello.c
localhost:~# ./check_comments hello.js
localhost:~# ./check_comments bench.py
```
