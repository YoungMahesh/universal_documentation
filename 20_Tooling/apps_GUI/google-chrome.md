Installation:

1. Visit: https://www.google.com/chrome/
2. Click 'Download Chrome'
3. Install `.deb` package with `sudo apt install ./<package-name>.deb`

Update:

```bash
sudo apt update
apt list --upgradable | grep chrome
sudo apt --only-upgrade install google-chrome-stable
```

### Enable Gemini sidebar on linux

1. Open URL: `chrome://flags/#glic`
   - Set Glic to Enabled.
2. Open URL: `chrome://flags/#geic-enabled`
   - If available, set Glic side panel to Enabled.
3. Click Relaunch.

### Increase font-size

Increase font-size (of chrome-UI: url-bar, bookmark-bar, tab-bar, etc):

```bash
# kill currently running google-chrome instances
killall -9 chrome google-chrome google-chrome-stable 2>/dev/null

# increase by form factor
# if you do this for one profile, it will automatically get applied to all other profiles you are going to open
google-chrome --force-device-scale-factor=1.2

# due to chrome UI increase, website size inside it also increases, to reduce that -
# 1. visit: chrome://settings/appearance
# 2. Page zoom: 90%
```
