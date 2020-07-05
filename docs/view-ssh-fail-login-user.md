```bash
$ cat /var/log/secure | awk '/Failed/{print $(NF-3)}' | sort | uniq -c | awk '{print $2" = "$1;}'
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY0NTY3MDYxM119
-->