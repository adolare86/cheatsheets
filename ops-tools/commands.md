
## Basic Linux Commands for day to day life

### ps

```
ps -ef --sort=%mem | head -n 10
ps -eo pid,%mem,%cpu,cmd --sort=-%mem | head -10
ps -eo pid,%mem,%cpu,cmd --sort=-%cpu | head -10
echo [PID]  [MEM]  [PATH] &&  ps aux | awk '{print $2, $4, $11}' | sort -k2rn | head -n 20
ps -eo pcpu,pid,user,args | sort -k 1 -r | head -10
```

### top
```
top -c -o %CPU
top -c -o %MEM
```

