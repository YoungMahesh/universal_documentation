```bash
gh repo list
gh repo create # open cli form for creation of github repository
gh repo create <org>/<repo-name> --private
gh repo delete OWNER/REPO

# -L == --limit; default limit 30
gh repo list -L 10
gh repo list <filter/organization-name>
# pull github repository
gh repo clone <owner>/<repo>
# check remote repository of current repository
gh repo view
# change default branch
gh repo edit --default-branch <branch-name>

# multiple github accounts
alias ghp='GH_CONFIG_DIR=$HOME/.config/gh-personal gh'

# run github action
# gh workflow run <file-name inside .github/workflows> --ref <branch-name>
gh workflow run build.yml --ref UI-improvements
# if you are running gh command from outside local repository, then you need to specify remote repository location
gh workflow run build.yml --repo <org-name>/<repo-name> --ref UI-improvements
# NOTE: If your workflow file is not on default branch, you may face error, 
#   in this case first merge minimum workflow file to default branch or temporarily change default branch
```

Credentials management:
You can give fine grained access to github cli by login through tokens, check [[github#Token Generation]]
```bash
gh auth login
# add repository deletion scope to `gh`
gh auth refresh -h github.com -s delete_repo
gh auth status
gh auth logout
```

Installation: https://cli.github.com/
