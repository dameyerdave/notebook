# Dia Diagram Editor

## Install on Mac OSX

```bash
brew install --cask dia
```

After his it won't run because DISPLAY=:0 env var is not set

```bash
vim /Applications/Dia.app/Contents/Resources/bin/dia
```

Add the following content to **line 40** (right before the `oascript` call)

```bash
#########################################################
# Ref: http://navkirats.blogspot.de/2014/10/dia-diagram-mac-osx-yosemite-fix-i-use.html
versionOSX=$(sw_vers -productVersion | awk -F '.' '{print $(NF-1)}')
[[ ${versionOSX} -ge 10 ]] && export DISPLAY=:0
#########################################################
```