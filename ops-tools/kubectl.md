
## kubectl Cheatsheet

### Pre configure

```
alias k=kubectl                         
export do="--dry-run=client -o yaml"    # k get pod x $do
export now="--force --grace-period 0"   # k delete pod x $now
```

