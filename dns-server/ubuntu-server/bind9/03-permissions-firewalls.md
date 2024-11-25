# PERMISSSIONS & FIREWALLS
  
  -

## Permissions of ports and services

  $ sudo ufw allow ssh

  $ sudo ufw allow 9090

  $ sudo ufw allow bind9

## Enable firewall (ufw)

  - Important! note: Be sure to give permissions at least to ports 22 and 9090 before activating the firewall because you may be left without access to the system

  $ sudo ufw enable
