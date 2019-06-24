# firewallsetup
## Fast Firewall Setup

This is a script for setting up a firewall with settings for tarpitting ssh and basic protections that everyone needs.

## Make the Rules Permenant
### Debian-based Distributions
sudo apt install iptables-persistent
sudo /etc/init.d/netfilter-persistent save

### Arch Linux Distributions
(Use iptable-save which is pre-installed)
sudo iptables-save

