# sshfs

## installation

	sudo apt-get install sshfs

mount:

	sudo sshfs -o allow_other,default_permissions root@192.168.1.24:/ /home/kaushal/Documents
umount:

	sudo umount /home/kaushal/Documents
