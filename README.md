# k3s-with-rancher-on-raspberry-pi

## Pre requisite before installing k3s

### Switching the kernel to 64-bit

> The assumption is you are on the latest Raspbian Buster to check run

`lsb_release -a`

> And you want to install all updates with

`sudo apt update
 sudo apt upgrade
`
> Now to verify the 64-bit kernel exists

`ls /boot/kernel8.img`

> Switching
> Add 64 bit = 1 at the end of the following file

`sudo nano /boot/config.txt`

> Now reboot to boot with the new, 64-bit kernel!
`sudo systemctl reboot`

> Verifying

`uname -a`
> if v8 is there then conversion is successful

### Prep to install k3s

> Configure legacy IP tables

```
sudo su -
sudo iptables -F
sudo update-alternatives --set iptables /usr/sbin/iptables-legacy
sudo update-alternatives --set ip6tables /usr/sbin/ip6tables-legacy
sudo reboot
```
> install k3s

```
 sudo su -
 curl -sfL https://get.k3s.io | K3S_KUBECONFIG_MODE="644" sh -s - --disable traefik
```

> Check for successful installation of k3s

`kubectl get nodes`
