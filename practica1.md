1
```localhost:~# grep -o '^[^:]*' /etc/passwd | sort```
2
```localhost:~# grep -v '^#' /etc/protocols | awk 'NF >= 2 {print $2, $1}' | sort -nr | head -5```
