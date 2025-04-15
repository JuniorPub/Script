```shell
#########################################################################################################################
#                                                                                                                       #
# EDIT BY       : Khaled                                                                                                #
# LAST UPDATE   : 15/04-2025                                                                                            #
# VERSION       : 1.0                                                                                                   #
# NOTES         : Basic router configuration layout                                                                     #
#                                                                                                                       #
#########################################################################################################################
```
 !----------------------------------------------!
 !-----------   Basic Configuration   ----------!
 !----------------------------------------------!

# Enable privileged EXEC mode
enable

# Enter global configuration mode
configure terminal

# General settings
no ip domain-lookup
hostname R1
banner motd # Unauthorized access to this device is prohibited! #

# Console configuration
line console 0
 password XXXXXXX
 login
 logging synchronous
 exec-timeout 60
exit

# VTY (Telnet/SSH) configuration
line vty 0 15
 password XXXXXXX
 transport input ssh
 login local
 logging synchronous
 exec-timeout 60
exit

# AUX line configuration
line aux 0
 password XXXXXXX
 login
 logging synchronous
 exec-timeout 60
exit

# SSH configuration
ip ssh version 2
ip ssh time-out 120

# Interface configurations
interface g0/0
 ip address 11.12.13.1 255.255.255.0
 description Connect to ITU
 no shutdown
exit

interface g0/1
 ip address 192.168.10.0 255.255.255.0
 description Connect to S1
 no shutdown
exit

# IPv6 and security settings
ipv6 unicast-routing
enable secret XXXXXXX
service password-encryption
security passwords min-length 10
login block-for 120 attempts 2 within 30

# Domain and cryptography configuration
ip domain-name KC.Local
username admin secret XXXXXXX
crypto key generate rsa 1024
exit

# Save configuration
write