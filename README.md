# firewallsetup
## Fast Firewall Setup

This is a script for setting up a firewall with settings for tarpitting ssh and basic protections that everyone needs.

## Download the rules to /etc/
```
git clone https://github.com/ChrisTitusTech/firewallsetup.git
```

## Enable the iptables systemd service
```
sudo systemctl enable --now iptables.service
```

## Make the Rules Permanant
### Debian-based Distributions
```
sudo apt install iptables-persistent
sudo /etc/init.d/netfilter-persistent save
```
### Arch Linux Distributions
*Use iptables-save which is pre-installed*
```
sudo iptables-save  >/etc/iptables/iptables.rules
sudo ip6tables-save >/etc/iptables/ip6tables.rules
```
### RHEL / CentOS Distributions
*This is by far the simpliest way to save rules and check them # chkconfig --list | grep iptables*

*Note: chkconfig iptables on only needs to be run once to turn the service on*
```
sudo chkconfig iptables on
sudo service iptables save
```
