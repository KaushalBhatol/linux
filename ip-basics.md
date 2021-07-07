# IP Basics

## Getting local Ip address

use any one command to know ip.

    nmcli -p device show
    ifconfig -a 
    ip a

## Getting Public Ip address

    curl ifconfig.me.
    host myip.opendns.com resolver1.opendns.com.

## Getting Site Ip

use any of one.

    host www.google.com
    dig www.google.com | awk '{print $1,$5}'
    dig google.com
