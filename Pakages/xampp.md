# Xampp Linux

## index

* [installation](#installation)
* [Creating Shortcut for command line](#creating-shortcut-for-command-line)
* [How to use](#how-to-use)
* [Changing htdocs directory](#changing-htdocs-directory)

## installation

first, you need to downlod [xampp for linux](https://www.apachefriends.org/index.html)

Now, make a downloded file exicutable:

```bash
 chmod +x xampp-linux-x64-8.0.7-0-installer.run
```

launch the installation file as root user:

```bash
sudo ./xampp-linux-x64-8.0.7-0-installer.run
```

## Creating Shortcut for command line

[Question answerd on askubuntu](https://askubuntu.com/a/1312385/1167010)

we using linking default xampp file to local fin

```bash
sudo ln -s /opt/lampp/xampp /usr/local/bin
```

* after applying ubove cammand you can use `xampp` insted of `/opt/lamp/xampp`

## How to use

* It quit simple commands after [created shortcut for command](#creating-shortcut-for-command-line)
* for starting all services: `sudo xampp start`
* for stoping all services: `sudo xampp stop`
* for starting apache only: `sudo xampp startapache`
* for stopping apache only: `sudo xampp soptapache`

## Changing htdocs directory

for changing directory we also use linking method.

1. move all `/opt/lampp/htdocs' files to your new directory
2. Use below command.

```bash
sudo rm -r /opt/lampp/htdocs
sudo ln -s ~/Documents/Learn/WEB/localhost/htdocs/ /opt/lampp/
```

* it linking all htdocs files into `/opt/lampp/htdocs` file
