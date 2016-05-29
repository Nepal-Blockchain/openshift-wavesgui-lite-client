# Openshift Wavesgui lite client
Wavesplatform GUI lite client on openshift 

https://github.com/wavesplatform/WavesGUI 

https://wavesplatform.com/

--
-- 

### Installation 
#### Using openshift web console (easy)
* Create an openshift app with php5.4 cartridge & add this repo as source code.
* Add cron1.4 cartridge in your app for auto updates. 

#### Using openshift client tools (rhc)
* `rhc app-create wavesgui php-5.4 cron-1.4 --from-code https://github.com/Nepal-Blockchain/openshift-wavesgui-lite-client.git`
* add `-n <your namespace>` if you've more than one namespace or..

--

#### Dont trust me? (You don't have to)

There are only two files in this repo

* post_deploy hook @ [/.openshift/action_hooks/post_deploy](../master/.openshift/action_hooks/post_deploy)
```shell
#!/bin/bash
cd  $OPENSHIFT_REPO_DIR
rm -r php
echo "Cloning Waves gui.."
git clone https://github.com/wavesplatform/WavesGUI.git php
```

* cron auto_update every 6 hours @ [/.openshift/cron/hourly/auto_update](../master/.openshift/cron/hourly/auto_update)
```shell
#!/bin/bash
hours=$(($(date +'%s / 60 / 60')))
if [[ $(($hours % 6)) -eq 0 ]]; then
cd  $OPENSHIFT_REPO_DIR
echo "Cloning Waves gui.."
rm -r php
git clone https://github.com/wavesplatform/WavesGUI.git php
fi
```
--

If you're feeling lazy..

> HTTP http://wavesgui-nepalbitcoin.rhcloud.com

For HTTPS you've to load/accept unsafe scripts coz the waves node IPs are on HTTP and so will throw mixed content error. (Hit `F12` to see that) 
> https://wavesgui-nepalbitcoin.rhcloud.com

> https://waves.npx.biz (cname/alias)

You can contact me @mtevx in https://wavesplatform.slack.com/ 

`<3 PEACE PEACE from Nepal`
