## Package Management Cheatsheet

### apt-get

```
# # Install or Upgrade an install package
apt-get install <package> 

# Remove files installed by <package>
apt-get remove <package> 

# Remove <package> and all the files it did create
apt-get purge <package>  

# Download package information from all configured sources
apt-get update

# Upgrade all packages installed on the system
apt-get upgrade

# Upgrade all packages installed on the system
apt-get upgrade

# Remove packages that were automatically installed to satisfy dependencies for other packages
apt autoremove

# Upgrade distribution
apt-get dist-upgrade
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
# Install deb package
dpkg -i <package file>

# Uninstall deb package
dpkg -P <package name>

# find all package with broken files
dpkg -C 

# find partially installed packages
dpkg -l | awk '/^iF/ {print $2}'

# Resolve file to package
dpkg -S /etc/vim/vimrc

# Package files
dpkg -L passwd

# Owned files
dpkg -c passwd

# Find packages by name
dpkg -l apache*

# Package details
dpkg -p passwd


```
