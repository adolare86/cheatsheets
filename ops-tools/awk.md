## awk cheatsheet

### awk

```
# Merge two lines into one line and sort num in last column
awk '{printf (NR%2==0) ? $0 "\n" : $0}' build_count_1 | awk '{print $NF,$0}' | sort -nr | cut -f2- -d' '

```
