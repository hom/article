```bash
$ cat /var/log/secure | awk '/Failed/{print $(NF-3)}' | sort | uniq -c | awk '{print $2" = "$1;}'
```