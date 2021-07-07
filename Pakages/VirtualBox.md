# [VirtualBox](https://www.virtualbox.org/)

## Index

* [installation](#installation)
* [installation of VirtualBox Extension Pack](#installation-of-virtualbox-extension-pack)
* [adding vboxusers on system](#adding_vboxusers_on_system)

## Installation

commands:

    sudo apt-get update
    sudo apt install -y virtualbox

## Installation of VirtualBox Extension Pack

* [download extension pack from official hear..](https://www.virtualbox.org/wiki/Downloads)
* open virtual box
* press `ctrl + g` key
* go to extanstion menu, press + icon rightside located
* select downloaded extanstion pack
* press install button, agree license
* enter linux password.

## Adding vboxusers on system

[answerd on askubuntu..](https://askubuntu.com/a/377781/1167010)

run this command:

    sudo usermod -a -G vboxusers $USER
    reboot
