# Router script
## Basic Conf 

```shell
enable
configure terminal 
no ip domain-lookup
hostname R1
banner motd #Unauthorized access to this device is prohibited!#
line console 0
password cisco12345!
login
logging synchronous
exec-timeout 60
exit
```


line vty 0 15
Password cisco12345!
transport input ssh
login local
logging synchronous
exec-timeout 60
exit

line aux 0
password cisco12345
login
logging synchronous
exec-timeout 60
Exit

ip ssh version 2
ip ssh time-out 120


interface g0/0
ip address 11.12.13.1 255.255.255.0
Description connect to ITU
no shutdown
exit

interface g0/1
ip address 192.168.10.0 255.255.255.0
Description connect to S1
no shutdown
Exit

ipv6 unicast-routing

enable secret R1
service password-encryption
security passwords min-length 10
login block-for 120 attempts 2 within 30

ip domain-name KC.Local
username admin secret R1!
crypto key generate rsa
1024
exit

write 
