# NetworkManager Scripts

> Run interface specific scripts on de/activating an interface with network manager.

This is a shameless rip-off from [rabin.io](https://blog.rabin.io/linux/networkmanager-using-dispatcher-d-to-run-scripts-based-on-network-connectivity).

On every connect/disconnect NetworkManager runs all scripts in the folder /etc/NetworkManager/dispatcher.d. This repository contains the **88-MASTER-DISPATCHER** script which gets the following two variables from NetworkManager:

```bash
$1 = Device name, e.g. ppp0, eth0
$2 = Connection State, up, down, vpn-up, vpn-down
```

Depending on the **STATE** and **CONNECTION_UUID** the script **88-MASTER-DISPATCHER** runs all scripts under **/etc/NetworkManager/dispatcher.d/$CONNECTION_UUID/$STATE/**

```bash
# tree /etc/NetworkManager/dispatcher.d

/etc/NetworkManager/dispatcher.d
├── 57874773-c8f2-4c37-966e-6caa756f1c5f
│   ├── vpn-down
│   │   └── enable-ipv6
│   └── vpn-up
│       └── disable-ipv6
|       └── mtr
├── 88-MASTER-DISPATCHER
```

You can get the connection uuid via nmcli.

```bash
nmcli --fields name,uuid -t connection show
Ethernet connection:73b56263-0306-463b-a179-1b86280950d4
wg-overlay:33a1412d-9172-47ac-b79e-d016d41d4721
docker0:3fb90a71-d42b-4521-949e-b2be16531f4f
Freifunk:22e4c57f-49fd-4de6-8762-fd5033140e2d
```

## Installation

```bash
git clone https://github.com/Madic-/NetworkManager-Scripts.git
cd NetworkManager-Scripts/
sudo cp -r scripts/* /etc/NetworkManager/dispatcher.d/
```

## Log

```bash
less /var/log/NetworkManager_dispatcher.d.log
```

## Further information

More information about the NetworkManager dispatcher can be found in the [Arch Wiki](https://wiki.archlinux.org/index.php/NetworkManager#Network_services_with_NetworkManager_dispatcher).
