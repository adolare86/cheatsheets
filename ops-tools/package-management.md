## Package Management Cheatsheet

### apt

```
# # Install or Upgrade an install package
apt install <package> 

# Remove files installed by <package>
apt remove <package> 

# Remove <package> and all the files it did create
apt purge <package>  

# Upgrade all packages
apt upgrade

# Upgrade distribution
apt dist-upgrade
```

### apt-cache
```
# Check if there is such a package name in the repos
apt-cache search <package> 

# Check which repos in which order provide the package
apt-cache policy <package>
apt-cache madison <packageName>
apt-cache show <packageName> | grep Version
aptitude show <packageName> | grep Version

# Information of all available package versions with dependancies
apt-cache showpkg <package_name>

# Remove all downloaded .debs
apt-cache clean

```


### apt-mark
```
# List all automatically installed packages
apt-mark showauto

# List all manually installed packages
apt-mark showmanual

# print a list of packages on hold
apt-mark showhold

```

### dpkg
```
# List all automatically installed packages
apt-mark showauto

# List all manually installed packages
apt-mark showmanual

# print a list of packages on hold
apt-mark showhold

```
