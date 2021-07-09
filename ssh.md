# ssh

## installation

	sudo apt-get update
	sudo apt-get install ssh -y

ssh are installed with openssh and sftp so you can use sftp for mounting your storage to other pc through lan.

## Genrating ssh

genrating normal rsa ssh key:

	ssh-keygen

## Configration on server

	cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
