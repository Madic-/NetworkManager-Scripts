# NetworkManager Scripts

Run scripts after activating a specific interface with network manager.

This is a shameless rip-off from [rabin.io](https://blog.rabin.io/linux/networkmanager-using-dispatcher-d-to-run-scripts-based-on-network-connectivity).

On every connect/disconnect NetworkManager runs all scripts in the folder /etc/NetworkManager/dispatcher.d.

NetworkManager will pass two variables to those scripts:

* $1 = Device name, e.g. ppp0, eth0
* $2 = Connection State, up, down, vpn-up, vpn-down

More information can be found in the [Arch Wiki](https://wiki.archlinux.org/index.php/NetworkManager#Network_services_with_NetworkManager_dispatcher).

Depending on these states and the CONNECTION_UUID the script 88-MASTER-DISPATCHER runs all scripts under e.g. /etc/NetworkManager/dispatcher.d/$CONNECTION_UUID/$2/*

```
# tree /etc/NetworkManager/dispatcher.d

/etc/NetworkManager/dispatcher.d
├── 57874773-c8f2-4c37-966e-6caa756f1c5f
│   ├── vpn-down
│   │   └── enable-ipv6
│   └── vpn-up
│       └── disable-ipv6
├── 88-MASTER-DISPATCHER
```

## Installation

git clone https://github.com/Madic-/NetworkManager-Scripts.git

sudo cp -r scripts/* /etc/NetworkManager/dispatcher.d/

## Log

/var/log/NetworkManager_dispatcher.d.log
