
## Basic Linux Commands for day to day life

### ps

```
ps -ef --sort=%mem | head -n 10
ps -eo pid,%mem,%cpu,cmd --sort=-%mem | head -10
ps -eo pid,%mem,%cpu,cmd --sort=-%cpu | head -10
```

### top
```
top -c -o %CPU
top -c -o %MEM
```

