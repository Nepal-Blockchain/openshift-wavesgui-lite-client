# Openshift Wavesgui lite client
Wavesplatform GUI lite client on openshift
### https://github.com/wavesplatform/WavesGUI
### https://wavesplatform.com/

--
There are only two files 
* post_deploy hook @ [/.openshift/action_hooks/post_deploy](../.openshift/action_hooks/post_deploy)
```shell
#!/bin/bash
cd  $OPENSHIFT_REPO_DIR
rm -r php
echo "Cloning waves gui.."
git clone https://github.com/wavesplatform/WavesGUI.git php
```
* cron auto_update every 6 hours @ [/.openshift/action_hooks/cron/auto_update](../.openshift/action_hooks/cron/auto_update)
```shell
#!/bin/bash
hours=$(($(date +'%s / 60 / 60')))
if [[ $(($hours % 6)) -eq 0 ]]; then
cd  $OPENSHIFT_REPO_DIR
echo "cloning waves gui.."
rm -r php
git clone https://github.com/wavesplatform/WavesGUI.git php
fi
```