# PROXMOX

## Index

* installation
  * [guide](#guide)
  * [Removing local_lvm storage](#removing-local-lvm-storage)
  * [Auto-turnoff display](#auto-turnoff-display)
  * [login via ssh key](#login-via-ssh-key)
* [Proxmox terminal in local terminal &#40;Using ssh&#41;](#proxmox-terminal-in-local-terminal-using-ssh)
* [VNC Client Access - Remote Display](#vnc-client-access---remote-display)
  * [Configure VNC Access via Monitor](#configure-vnc-access-via-monitor)
  * [Configure VNC Access via Configuration File](#configure-vnc-access-via-configuration-file)

## Installation

### Guide

* Download Proxmox Virtual Environment from [hear](https://www.proxmox.com/en/downloads).
* Use [balenaEtcher](https://www.balena.io/etcher/) for creating bootable usb.
* Botting through usb and installation was so easy..
* NOTE: you can give any name in host name just use dot
  * ex : kaushal.server
* NOTE: Input diffrent ip which your router not assigned to other device.
  * ex : 192.168.1.24
  * also change only last dot after numbers
  * Like : 00.00.00.3 to 00.00.00.24 (hear 00 showing your ip, it was any number so ignore 00.)
* after installation go to another pc browser and go to ip addres which you assigned wehen istalling.. also it showen on that laptop
* or use command

```bash
firefox https://192.168.1.24/
```

### Removing local lvm storage

For Fully remove `local_lvm` use below method:

1. remove local_lvm from host > storage, through browser
2. Open proxmox terminal and run below command

```bash
lvremove /dev/pve/data
lvresize -l +100%FREE /dev/pve/root
resize2fs /dev/mapper/pve-root
```

### Auto-turnoff display

```bash
nano /etc/systemd/logind.conf
```

edit below lines and also remove `#` from edited lines

```txt
HandleLidSwitch=ignore
HandleLidSwitchDocked=ignore
```

Now resrarting systemd-login :

```bash
systemctl restart systemd-logind.service
nano /etc/default/grub
```

Change below lines from grub :

```txt
GRUB_TIMEOUT=0
GRUB_CMDLINE_LINUX="consoleblank=100"
```

Updating grub & system reboot :

```bash
update-grub
reboot
```

### login via ssh key

* for login without password you need ssh key.
* this key is gerated on primery pc which is your pc __not a proxmox server pc__.

[fore more details of ssh key click hear..](https://www.ssh.com/academy/ssh/keygen)

Gerating ssh key:

* open terminal use below code

```bash
ssh-keygen -f ~/proxmox -t ecdsa -b 521
```

* press enter again and agian store that key on default location.
* default location is `~/.ssh`

Copying the Public Key to the Server:

  ssh-copy-id -i ~/.ssh/proxmox.pub root@192.168.1.24 # enter server password
  ssh root@192.168.1.24
  rm -r ~/.ssh/id_*

Once the public key has been configured on the server, the server will allow any connecting user that has the private key to log in. During the login process, the client proves possession of the private key by digitally signing the key exchange.

## Proxmox terminal in local terminal Using ssh

for using proxmox terminal by ssh you just need run to below command.

```bash
ssh root@192.168.1.1
```

## VNC Client Access - Remote Display

[For Official Proxmox VNC guidence click hear..](https://pve.proxmox.com/wiki/VNC_Client_Access)

* we have two mathedos for do thet
  1) using terminal ( Perminante )
  2) using dispalay menu

### Configure VNC Access via Monitor

* Go to VM´s 'Monitor' panel in the web interface.
* You can setup a plain VNC or also a password secured one:
  * for the plain one type the following into the monitor:
  * `change vnc 0.0.0.0:75`

75 denotes the port, this will get added to the VNC base port of 5900, so in this case the VNC server listens on all addresses on port 5975.

* for the password secured one type the following into the monitor:

```bash
change vnc 0.0.0.0:75,password
set_password vnc foobar1
expire_password vnc +30
```

note: the first "password" parameter after the IP address mustn't be replaced by a password but is the word "password" itself, this is just a boolean parameter telling QEMU that the server needs a password.

### Configure VNC Access via Configuration File

* Add in the VM´s configuration file /etc/pve/local/qemu-server/<KVM_ID>.conf a line which specifies the VNC display number as follows ("77" in the example below):

```php
args: -vnc 0.0.0.0:77
```

* The display number can be freely chosen, but each number must occur only once. VNC service listens then at port 5900+display_number. Note that connections via noVNC start using display number 0 consecutively therefore it´s recommended to use higher numbers in order to avoid conflicts.
* Connect from VNC client to Proxmox host ip address and port as specified (5977 in the above example)

## sftp

Managing files through ftp:

```bash
sftp://ip/root  # safe
sftp://ip/# full / directory
sftp://ip/var/lib/vz/template/iso #iso directory
```

using one of above sftp method you can got directory.

mount sftp as local folder:

```bash
sudo apt-get install sshfs
sudo sshfs -o allow_other root@192.168.1.24:/root/ /home/kaushal/Documents/Server-Storage
```

unomount sftp:

```bash
sudo umount Documents/Server-Storage
```

## Proxmox update

For getting updates without any errors, we need to remove enrerprice repository.

removing enterprice repository :

```bash
rm -r /etc/apt/sources.list.d/pve-enterprise.list
apt update
```

## Proxmox Paths and Locations of files

```bash
/var/lib/vz/dump # ISO Files
/var/lib/vz/template/iso # Images
/var/lib/vz/images # Templates
/var/lib/vz/template/cache # Cache
```
