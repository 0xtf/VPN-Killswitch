# VPN-Killswitch
A killswitch for Network Manager based on VPN Profile

## The idea

I have a VPN profile configured for when I'm in *hostile environments*. Problem with VPN is that it can drop, and while it's off, we'll eventually leak information over the unprotected network. The idea behind this project is to provide a killswitch that is only enabled when using a specific VPN profile in Network Manager.

## Compatability 

This has been tested in Ubuntu 18.04. If you try it and it works well in other versions or distros, let me know. 

## Install

Before we can use the dispatcher functionality of Network Manager, we need to first enable the dispatcher service *(which is disabled by default)*.

```
systemctl enable NetworkManager-dispatcher.service
```

After that you'll be able to prepare everything:

* Download **VPN-Killswitch** and **VPN-Monitor**
* Make them both executable
* Change the interface being used in **VPN-Killswitch** in variable **VPNIFACE**
* Change the interface being used in **VPN-Monitor** *(variable **VPNIFACE**)*, the VPN profile name *(variable **PROFILE**)* and the **VPN-Killswitch** location *(variable **PATH**)*
* Move **VPN-Monitor** to **/etc/NetworkManager/dispatcher.d/VPN-Monitor**

## Testing & Troubleshooting

grep'ing syslog will let you know if the killswitch is enabled or not: **grep VPN-Killswitch /var/log/syslog**

## Getting out of the fail safe mode

After VPN-Monitor enables the killswitch, it will be on until you turn it off *(that includes reboots)*. To clear its state, run:

```
sudo $PATH/VPN-Killswitch -c 
```

## Questions, comments or concerns

Feel free to open an issue or ping me on [Twitter - @0xtf](https://twitter.com/0xtf).
