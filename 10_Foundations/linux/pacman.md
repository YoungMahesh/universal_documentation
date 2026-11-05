```sh
# install package
# -S = sync
pacman -S gvim

# refresh package database and install package
# -y = refresh
pacman -Sy gvim

# refresh pkg database, upgrade all packages to newer version, install new package
# - u = Upgrades all installed packages to available newer versions
pacman -Syu gvim
```

| Option | Meaning | Purpose                                                |
| ------ | ------- | ------------------------------------------------------ |
| `-Q`   | Query   | Query installed packages                               |
| `-i`   | Info    | Display detailed package information                   |
| `-S`   | Sync    | Work with packages in remote repositories              |
| `-y`   | Refresh | Refresh the local package database from repositories   |
| `-u`   | Upgrade | Upgrade installed packages to newer available versions |
