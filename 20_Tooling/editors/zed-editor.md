### activate python environment in terminal

Methods:

1. open .py file, then open terminal
2. run `source .venv/bin/activate`

### search filter

Currently, zed editor does not have search filter settings, you can filter files from global search as follows:

1. Open global search (`ctrl-shift-f`)
2. click on filter-icon
3. past file-path regex in 'Exclude' section: `env/*, *lock.yaml, *svg, *json, *factory.ts, *css`

### update settings

View global settings:

- `zed: open default settings`

Update global settings:

- `zed: open settings`

Update project settings:

- put settings in `.zed/settings.json` file of the project to update settings for the project

---

### update keymap

View default keymaps:

- `zed: open default keymap`
- `vim: open default keymap`

Update global keymaps:

- `zed: open keymap file`

---

### remove cache

- this helped when there was suddenly a blank-space on left and right side of main editor

```bash
rm -rf ~/.local/share/zed/db
```
