# Windows Fundamentals

# netstat
> netstat –naob (o=owning process, b = executable)
> netstat –aob (no resolution)
> netstat –vb (nice formatting)
> netstat –a –p TCP –q 5
# powershell
> Get-nettcpconnection | ?{$_.state –like “*Established*”}

# Firewall logs
> Get-content c:\windows\system32\LogFiles\HTTPERR\httperr1.log
> $fw = Get-content c:\windows\system32\logfiles\pfirewall.log
> Foreach($f in $fw){$dst = $f.split(“ ”);$dst[5]}

#arp table maps and caches ip’s to mac addresses
> arp –a
# powershell
> Get-netneighbor –addressfamily ipv4

# Controls the routing on the local device
> Route Print
> Route print -4
> Route Print -6
# Also prints routes
> Get-netroute
> $routes = get-netroute
> $routes.AddressFamily | get-unique

# DNS
# ipconfig 
> Ipconfig /displaydns
> More %SystemRoot%\System32\Drivers\etc\hosts
# powershell
> get-DnsClientCache

# Processes
# wmic
> Wmic process list
> Wmic job list brief
# tasklist
Tasklist /M /FO TABLE
# powershell
> $m = (Get-process).modules |Sort-Object –property ModuleName


# Services
# wmic
> Wmic startup list brief
# tasklist
Tasklist /SVC /FI “STATUS eq running”
#sc (cmd.exe) ->drivers
Sc query type= driver
# powershell
get-service |?{$_.status –eq “stopped” –and $_StartType –eq “Automatic”}

# System Configs

> Ifconfig /all
> Set or Get-variable
> Net users
> Net localgroup administrators
> Wmic qfe list
> Cipher
> Net view
> Wmic computersystem get manufacturer
> Wmic product list

# Logs
# wevtutil
> Wevtutil el
> Wevtutil gli security
> Wevtutil qe security /f:text (this is a lot)

# powershell
> Get-winevent –logname security –maxevents 10
> get-winevent –logname security | ?{$_.Message –like “*cmd*”}

# Files
$date = (get-date).adddays(-1)
Get-childitem c:\windows |?{$_.lastwritetime –ge $date}

# Firewalls
# Netsh 
> Netsh wlan show interfaces
> Netsh firewall show portopening
> Netsh firewall show allowedprogram
> Netsh advfirewall firewall show rule name=all
# powershell
> get-netfirewallportfilter
> get-netfirewalladdressfilter

# Defender
> Get-mppreference
> Get-mpcomputerstatus
> Get-mpthreat
![image](https://user-images.githubusercontent.com/21697803/114831732-b65d6d80-9d9b-11eb-98d7-1ec15a3e5060.png)


# Self Paced Lab Time
Unzip if required the cantinwindow4.exe
Open an adminstrative command prompt
Change to the correct directory and run the file.

There are a number of things going on, try to identify all the files, and the changes the the operating systema that were made.
Leverage all the tools we discussed to idenfity what ironcat is up to this time.
