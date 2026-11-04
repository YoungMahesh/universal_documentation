#cli/password #encryption 

```bash
# view/edit
pass   # list all passwords
pass generate aws    # generate and store a new password
openssl rand -hex 10  # generate 10-char, hex-encode password
pass github/personl  # print content of 'github/personal'
pass github/personal -c  # copy first-line/password to clipboard
pass rm github/personal  # remove password/file
pass git revert HEAD   # remove last changes
pass git log  # changes made until now
pass edit github/personal  # create/edit password/file
export EDITOR=nvim  # append this to ~/.bashrc file to set neovim as default editor

# search
pass find github  # search word `github` in file-path
pass grep email   # search word `email` within file-content

# if you are getting warnging: There is no assurance this key belongs to the named user: change trust of gpg-key as mentiond in ./encryption.md

# every edit, remove, generate, insert command of pass creates a new git-commit
# revert helps when you want to revert last update you made in `pass`

# lock pass content immediately by restarting gpg
gpg-connect-agent reloadagent /bye
```

### initialize
```bash
# create or import gpg keys: read `encryption.md` file
gpg -k  # get gpg keys
# pub   rsa3072 2023-09-11 [SC] [expires: 2025-09-10]
#      525A4CCA5D86AE842D9A51C3DF39BF4C371A2ADD
# rsa3072 - cryptography-algorithm-name
# 525....ADD - gpg-public-key

# Trust gpg key. 
# NOTE: you can decrypt/view existing passwords with untrusted key, 
#   but to store new passwords it is necessary to trust gpg key 
gpg --edit-key <KEY_ID>
gpg> trust            
Your decision? 5
Do you really want to set this key to ultimate trust? (y/N) y
gpg> quit
 
sudo apt install pass

# set password-directory, to make this location permanent, add this command
#   to ~/.bashrc
# If you don’t set anything, pass uses: ~/.password-store
export PASSWORD_STORE_DIR="$HOME/secure/password-store"

# create new password-store
pass init <gpg-public-key> # set/change gpg-key for password-store
cat ~/.password-store/.gpg-id  # view gpg-public-key used to encrypt passwords

# create new git repository
pass git init
# OR use existing password-store
git clone <pass-repository-url> ~/.password-store  # here we are cloning pass-repo in `.password-store`
```

### multiple pass
1. login to a different user account: `su -l <username>`

2. append to `.bashrc` file
    ```bash
    # set nvim as default editor for pass
    export EDITOR=nvim

    # need to execute `script /dev/null` to make pass work in other user-account shell
    # following script automatically execute `script /dev/null` on login
    if [ -z "$SCRIPT" ]; then
        SCRIPT=/dev/null script -q
    fi
    ```

- create new user if not already availble
    ```bash
    su -l <username> # login to diffrent user
    # setup new user on your ubuntu computer 
    useradd -m <username>  # create a new user
    passwd <username>  # set password for user
    ```
