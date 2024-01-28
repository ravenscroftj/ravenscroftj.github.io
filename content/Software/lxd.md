---
tags: 
 - software
---
# LXD

A daemon for managing virtual machines on Linux. Works best with [[qemu]].

## Installing dependencies

Install lxd from snap on ubuntu and dependent libraries:

`sudo apt install qemu-kvm virt-viewer`

virt-viewer is a tool for connecting and talking to hosted machines.

## Installing Windows 11

### Install without network/internet

From this guide[^1]:

1. At the point where Win 11 tries to force you onto the internet enter Shift + F10 and type `OOBE\BYPASSNRO` - this will reboot the installer.
2. At the same point during the boot process after this step, the installer will let you pass if you click "I don't have internet" and then "Continue with limited setup".


### Docker Network Interference

To prevent Docker from interfering with networks in LXD you need to configure the firewall [^dockerFirewall].

```shell
iptables -I DOCKER-USER -i lxdbr0 -j ACCEPT
iptables -I DOCKER-USER -o lxdbr0 -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
```

### Spice Client

Install `sudo apt-get install gir1.2-spiceclientgtk-3.0`

### Guest Tools

For best results, install [spice guest tools](https://www.spice-space.org/download/binaries/spice-guest-tools/) which provides a bunch of tooling inside the VM that can be used by the parent machine.

[^1]: https://pureinfotech.com/bypass-internet-connection-install-windows-11/

[^dockerFirewall]: https://linuxcontainers.org/lxd/docs/master/howto/network_bridge_firewalld/#prevent-issues-with-lxd-and-docker

https://github.com/bmullan/Windows-VM-RemoteApp-Configuration-Guide-for-Ubuntu/blob/master/LXD%20Windows%20VM%20and%20RemoteApp%20Configuration%20Guide.pdf

https://discuss.linuxcontainers.org/t/running-virtual-machines-with-lxd-4-0/7519