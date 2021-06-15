# ftp server host

* Access to an FTP server can be managed in two ways
  * [Anonymous](#Anonymous-FTP-Configuration)
  * Authenticated

## vsftpd - FTP Server Installation

vsftpd is an FTP daemon available in Ubuntu. It is easy to install, set up, and maintain. To install vsftpd you can run the following command:

```bash
sudo apt install vsftpd 
```

## start or stop

```bash
sudo systemctl start vsftpd.service 
sudo systemctl stop vsftpd.service 
sudo systemctl restart vsftpd.service 
```

## Anonymous FTP Configuration

By default vsftpd is not configured to allow anonymous download. If you wish to enable anonymous download edit `/etc/vsftpd.conf` by changing:

```txt
anonymous_enable=YES
```

## ftp default location and directory

* During installation a ftp user is created with a home directory of `/srv/ftp`. This is the default FTP directory.

* If you wish to change this location, to `/srv/files/ftp` for example, simply create a directory in another location and change the ftp user’s home directory:

```bash
sudo mkdir -p /srv/files/ftp
sudo usermod -d /home/kaushal ftp 
```

After making the change restart vsftpd:

```bash
sudo systemctl restart vsftpd.service
```

Finally, copy any files and directories you would like to make available through anonymous FTP to `/srv/files/ftp`, or `/srv/ftp` if you wish to use the default.

## User Authenticated FTP Configuration

By default vsftpd is configured to authenticate system users and allow them to download files. If you want users to be able to upload files, edit `/etc/vsftpd.conf`:

```txt
write_enable=YES
```

Now restart vsftpd:

```txt
sudo systemctl restart vsftpd.service
```

Now when system users login to FTP they will start in their *home* directories where they can download, upload, create directories, etc.

Similarly, by default, anonymous users are not allowed to upload files to FTP server. To change this setting, you should uncomment the following line, and restart vsftpd:

```txt
anon_upload_enable=YES
```

> Warning :
Enabling anonymous FTP upload can be an extreme security risk. It is best to not enable anonymous upload on servers accessed directly from the Internet.

The configuration file consists of many configuration parameters. The information about each parameter is available in the configuration file. Alternatively, you can refer to the man page, **man 5 vsftpd.conf** for details of each parameter.

## Securing FTP

There are options in __/etc/vsftpd.conf__ to help make vsftpd more secure. For example users can be limited to their home directories by uncommenting:

```txt
chroot_local_user=YES
```

You can also limit a specific list of users to just their home directories:

```txt
chroot_list_enable=YES
chroot_list_file=/etc/vsftpd.chroot_list
```

After uncommenting the above options, create a __/etc/vsftpd.chroot_list__ containing a list of users one per line. Then restart vsftpd:

```txt
sudo systemctl restart vsftpd.service
```

Also, the __/etc/ftpusers__ file is a list of users that are disallowed FTP access. The default list includes root, daemon, nobody, etc. To disable FTP access for additional users simply add them to the list.

FTP can also be encrypted using FTPS. Different from SFTP, FTPS is FTP over Secure Socket Layer (SSL). SFTP is a FTP like session over an encrypted SSH connection. A major difference is that users of SFTP need to have a shell account on the system, instead of a nologin shell. Providing all users with a shell may not be ideal for some environments, such as a shared web host. However, it is possible to restrict such accounts to only SFTP and disable shell interaction.

To configure FTPS, edit __/etc/vsftpd.conf__ and at the bottom add:

```txt
ssl_enable=YES
```

Also, notice the certificate and key related options:

```txt
rsa_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem
rsa_private_key_file=/etc/ssl/private/ssl-cert-snakeoil.key
```

By default these options are set to the certificate and key provided by the ssl-cert package. In a production environment these should be replaced with a certificate and key generated for the specific host. For more information on certificates see [Security - Certificates](https://ubuntu.com/server/docs/security-certificates).

Now restart vsftpd, and non-anonymous users will be forced to use FTPS:

```txt
sudo systemctl restart vsftpd.service
```

To allow users with a shell of /usr/sbin/nologin access to FTP, but have no shell access, edit /etc/shells adding the nologin shell:

```bash
# /etc/shells: valid login shells
/bin/csh
/bin/sh
/usr/bin/es
/usr/bin/ksh
/bin/ksh
/usr/bin/rc
/usr/bin/tcsh
/bin/tcsh
/usr/bin/esh
/bin/dash
/bin/bash
/bin/rbash
/usr/bin/screen
/usr/sbin/nologin
```

This is necessary because, by default vsftpd uses PAM for authentication, and the __/etc/pam.d/vsftpd__ configuration file contains:

```txt
auth    required        pam_shells.so
```

The shells PAM module restricts access to shells listed in the /etc/shells file.

Most popular FTP clients can be configured to connect using FTPS. The lftp command line FTP client has the ability to use FTPS as well.

## References

* See the [vsftpd website](http://vsftpd.beasts.org/vsftpd_conf.html) for more information.
