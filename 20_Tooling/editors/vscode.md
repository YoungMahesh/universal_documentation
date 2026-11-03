[[vscode-keymaps]]
[[vscode-extensions]]

### basic interaction

[[editor-keymaps#vscode keymaps]]

```bash
#------------------- Explorer/Files-section ---------------------------
Cntr + E  # move to files/explorer-section
j         # move downward in explorer
k         # move upward in explorer
Cntr + `  # move to terminal

#------------------- Global search ---------------------------
Cntr + Shift + f # search text in all files of opened directory
Fn4              # move forward in global search results
Shift + Fn4      # move backward in global search results
Enter            # move cursor to current global search result

#--------------------- Text Editor ----------------------------------
Cntr + 1    # move to text editor
Cntr + p    # search files by name in current directory
Cntr + P    # open command palette
```

### installation

```sh
# install vscode
snap install code --classic
# check if update is available
snap refresh --list
# upgrade vscode
snap refresh code
```

### disable syntax warnings

- sometimes to review code, we download it and read it inside vscode without installing dependencies like node_modules, if code is written in typescript or javascript then it leads to syntax warnings in vscode
- we can disable those warning by
  1. open command pallete (`Cntr + Shift + p`)
  2. open workspace settings (JSON)
  3. disable typescript and javscript validation by adding these lines

```json
"typescript.validate.enable": false,
"javascript.validate.enable": false,
```
