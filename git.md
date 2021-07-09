## Git

## installation

	sudo apt-get update
	sudo apt-get install git -y

## Basic


* configraton for not asking username and password every time

first genrate ssh key and paste it on github.com settings/ssh

after run below commands on repository directory :

	git remote set-url origin git@github.com:KaushalBhatol/linux.git
	git config --global credential.helper store
hear KaushalBhatol/linux.git is repository location.
