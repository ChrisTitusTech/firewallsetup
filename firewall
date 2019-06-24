#!/bin/bash
#
# iptables example configuration script

# Drop ICMP echo-request messages sent to broadcast or multicast addresses
echo 1 > /proc/sys/net/ipv4/icmp_echo_ignore_broadcasts

# Drop source routed packets
echo 0 > /proc/sys/net/ipv4/conf/all/accept_source_route
 
# Enable TCP SYN cookie protection from SYN floods
echo 1 > /proc/sys/net/ipv4/tcp_syncookies
 
# Don't accept ICMP redirect messages
echo 0 > /proc/sys/net/ipv4/conf/all/accept_redirects
 
# Don't send ICMP redirect messages
echo 0 > /proc/sys/net/ipv4/conf/all/send_redirects
 
# Enable source address spoofing protection
echo 1 > /proc/sys/net/ipv4/conf/all/rp_filter
 
# Log packets with impossible source addresses
echo 1 > /proc/sys/net/ipv4/conf/all/log_martians
 
# Flush all chains
/sbin/iptables --flush
 
# Allow unlimited traffic on the loopback interface
/sbin/iptables -A INPUT -i lo -j ACCEPT
/sbin/iptables -A OUTPUT -o lo -j ACCEPT
 
# Set default policies
/sbin/iptables --policy INPUT DROP
/sbin/iptables --policy OUTPUT DROP
/sbin/iptables --policy FORWARD DROP
 
# Previously initiated and accepted exchanges bypass rule checking
# Allow unlimited outbound traffic
/sbin/iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
/sbin/iptables -A OUTPUT -m state --state NEW,ESTABLISHED,RELATED -j ACCEPT
 
#Ratelimit SSH for attack protection
/sbin/iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --update --seconds 60 --hitcount 4 -j DROP
/sbin/iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --set
/sbin/iptables -A INPUT -p tcp --dport 22 -m state --state NEW -j ACCEPT
 
# Allow certain ports to be accessible from the outside
/sbin/iptables -A INPUT -p tcp --dport 25565 -m state --state NEW -j ACCEPT  #Minecraft
/sbin/iptables -A INPUT -p tcp --dport 8123 -m state --state NEW -j ACCEPT   #Dynmap plugin

# Other rules for future use if needed.  Uncomment to activate
# /sbin/iptables -A INPUT -p tcp --dport 80 -m state --state NEW -j ACCEPT    # http
# /sbin/iptables -A INPUT -p tcp --dport 443 -m state --state NEW -j ACCEPT   # https

# UDP packet rule.  This is just a random udp packet rule as an example only
# /sbin/iptables -A INPUT -p udp --dport 5021 -m state --state NEW -j ACCEPT

# Allow pinging of your server
/sbin/iptables -A INPUT -p icmp --icmp-type 8 -m state --state NEW,ESTABLISHED,RELATED -j ACCEPT

  
# Drop all other traffic
/sbin/iptables -A INPUT -j DROP

# print the activated rules to the console when script is completed
/sbin/iptables -nL
