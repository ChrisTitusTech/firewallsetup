# firewallsetup
## Fast Firewall Setup

This is a script for setting up a firewall with settings for tarpitting ssh and basic protections that everyone needs.

## Download the rules to /etc/
```
git clone https://github.com/ChrisTitusTech/firewallsetup.git
````
## Make the Rules Permenant
### Debian-based Distributions
```
sudo apt install iptables-persistent
sudo /etc/init.d/netfilter-persistent save
```
### Arch Linux Distributions
*Use iptable-save which is pre-installed*
```
sudo iptables-save > /etc/iptables/iptables.rules
```
### RHEL / CentOS Distributions
*This is by far the simpliest way to save rules and check them # chkconfig --list | grep iptables*

*Note: chkconfig iptables on only needs to be run once to turn the service on*
```
sudo chkconfig iptables on
sudo service iptables save
```
