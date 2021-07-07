# Osintgram

* Used for knowing details of user folowers and followings
* you can get number and email also of user followers
* also able to download storys and profile pics

## installation

	sudo apt-get install -y git python3 pip libncurses5-dev
	sudo pip install geopy gnureadline==6.3.3
	git clone https://github.com/Datalux/Osintgram.git
	cd Osintgram
	sudo pip install -r ./requierments.txt

## configration

* open `config/credentials.ini` or run `make setup`
* Enter any instagram account username and password
* Ensure that account is not your personal account, Because accont shoud be banned if instagram detacted activity.

## Use

	python3 main.py --help
	python3 main.py kaushal_bhatol
	python3 main.py list  # show all atacks command

Note: kaushal_bhatol was target username you can change accroding your way.
