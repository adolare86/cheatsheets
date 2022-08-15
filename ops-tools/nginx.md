## Nginx Cheatsheet

### nginx commands

```
# Check if Nginx configuration is ok
nginx -t

# Gracefully reload NGINX processes
nginx -s reload

# Dump full NGINX configuration
nginx -T

# Display nginx help menu
nginx -g

# After config change, test and reload
nginx -t && nginx -s reload

# Detailed information
nginx -V
```
