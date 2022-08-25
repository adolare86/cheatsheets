
## sed cheatsheet

### sed

```
# Insert a line in a string after finding a match
echo "This is test" | sed 's/test/& are you testing?/'

# Insert a line after a particular line number using the “a”
sed '2 a This is test' test.txt

# Insert a line after the last line using the “a”
sed '$ a This is test' test.txt

# Insert a line anywhere in the file after matching a pattern using the “a”
sed -i '/^    acm_arn.*/a \    web_acl_id                  = data.aws_wafv2_web_acl.waf-cloudfront.arn' main.tf

# Insert multiple lines after the matching pattern using “a”
sed '/^[a-c]/a test1\ntest2' test.txt

# Insert a line before  matching a pattern using the “I”
sed '/update/i This is test' test.txt
```

