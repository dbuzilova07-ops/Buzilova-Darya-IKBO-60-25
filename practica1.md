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
#!/bin/sh
grep -oE '[A-Za-z_][A-Za-z0-9_]*' "$1" | sort -u | tr '\n' ' '
printf '\n'

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
 
for file in $(find . -type f \( -name "*.c" -o -name "*.js" -o -name "*.py" \))
do
    case "$file" in
        *.c|*.js)
            if head -1 "$file" | grep -qE '^(//|/\*)'
            then
                echo "$file: comment"
            fi
            ;;
        *.py)
            if head -1 "$file" | grep -q '^#'
            then
                echo "$file: comment"
            fi
            ;;
    esac
done

localhost:~# chmod +x check_comments
```
7
```bash
#!/bin/sh
for file in $(find "$1" -type f)
do
        hash=$(md5sum "$file" | awk '{print $1}')
        for other in $(find "$1" -type f)
        do
                if [ "$file" != "$other" ]
                then
                        other_hash=$(md5sum "$other" | awk '{print $1}')
                        if [ "$hash" = "$other_hash" ]
                        then
                                echo "$file <-> $other"
                        fi
                fi
        done
done

localhost:~# chmod +x duplicates
localhost:~# ./duplicates .
./hello.c <-> ./copy.c
./copy.c <-> ./hello.c
```
8
```bash
#!/bin/sh
dir="$1"
ext="$2"
find "$dir" -type f -name "*.$ext" > /tmp/filelist.txt
tar -cf archive.tar -T /tmp/filelist.txt
rm /tmp/filelist.txt

localhost:~# chmod +x archiver
localhost:~# ./archiver . c
```
9
```bash
#!/bin/sh
sed 's/    /\t/g' "$1" > "$2"
 
localhost:~# chmod +x tabs
```
10
```bash
#!/bin/sh
find "$1" -type f -empty

localhost:~# chmod +x empties
localhost:~# ./empties .
```
