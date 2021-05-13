# Linux Fundamentals

# Netstat
> netstat –naovp
> netstat –aovp (no resolution)
> netstat -le
> netstat –lec | grep 8000

# Tcpdump

> tcpdump –i <eth0> 
> tcpdump -n
> tcpdump –i <eth0> -w pcap1.pcap
> tcpdump -n –r pcap1.pcap | cut –d “ “ –f 3| cut –d “.” –f 1,2,3,4

#arp table maps and caches ip’s to mac addresses
arp –av

# Controls the routing on the local device
> route –ve
> route –ven (no name resolution)

# Also prints routes
> netstat –rv
> netstat –rvn

# Controls the routing on the local device
> systemd-resolve --statistics
> systemd-resolve --status
> cat /etc/resolv.conf
> cat /etc/hosts 

# ps
> ps –e (e is often for “extended”)
> ps -ef or ps –aux
> pstree –a
> ps –u <user> - u <user> u
> ps –q <pid>
> pmap <pid> 
> docker ps –a (don’t forget about docker)

# lsof
> lsof –i 4
#ls
> ls -ltrR  (|grep <date> or <filename>)
# whereis
> whereis –b <file name>
# find
> find . –maxdepth 1 –mmin -60

# System Configs

> ifconfig / Ip Addr
> printenv
> hostname
> whoami
> id
> logname
> uptime
> uname –a
> cat /proc/version
> cat /proc/cpuinfo
> cat /proc/cmdline
> cat /etc/passwd && cat /etc/shadow

# Logs

## Auth.log
> ls –l /var/log/
> cat /var/log/auth.log
> cp /var/log/auth* /opt/response/
> cat /var/log/auth.log | grep session | cut –d “ “ –f 1,2,3,7-20

## Syslog
> ls –l /var/log
> cat /var/log/syslog
> cp /var/log/syslog*
> cat /var/log/syslog | grep cron

# Apache access logs (after ssl decryption)
> ls -l /var/log/apache/access.log
> cat /var/log/apache/access.log

# Now you are a manual WAF
> cat /var/log/apache/access.log|grep “whoami”

# Services
> service –status-all (most nix)
> ls /etc/rc*.d (solaris)
> chkconfig –list (redhat)

# iptables firewall
> iptables –-list 
 
# Scheduled Tasks
> ls –r /etc/cron*
> cat /var/spool/cron/crontabs/*


Self Paced Lab Time!
Cd into the /home/ubuntu/spplab folder
sudo ./catvsbeaver&

Use these tools to find out whats going on here! What Happened?
What files were created?
Is anything running now?
