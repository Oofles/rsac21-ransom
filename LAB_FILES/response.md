# Response

## Get ready! 
1. Open wireshark and begin capturing to a c:\ location.
2. Open Procmon

## Launch!


Open process explorer
Open wireshark and start capturing
Disable defender and real time protections


1. Open Internet explorer
3. Browse to the ip where you are hosting the malware from the creation device.
4. Click the file to download it.
5. Open and administrative command prompt
6. Change directories to the files location
7. Run ironcatrsa.exe
`ironcatrsae.exe encrypt <custom password>
8. Watch it run.

## Now Respond As if you weren't the one who did it!
1. Turn off wireshark capture and save the pcap.
2. Inspect process explorer activity.
3. Use the [Windows Fundamentals](windows_fundamentals.md) resource to look for various indicators of activity.

## Files, Files,Files
Don't close the the cmd prompt.
ctrl+c. 
Use the history command to find the command line arguments used.

Get as much information from the ransomnote as possible>
What is the size and file type. When was it created, and last modified or access and who owns it?
`powershell get-file`
Use this information to find other effected files on the system. For this lab just focus on users.
This can be used as a detection across multiple devices to find te total impact of the incendent. Log multiple machines by time stampe and you can build the attackers path.
Remote example.

## Analyze the packet capture. And track down that pesky activity.
Netstat to find activity.
Now track that to the pid.
Now track the pid to the process information and find the file reponsible. Look at the time stampe. Maybe other files were modified here too?

## Log analysis
Event view shows all logs cleared.  So you can't get the command line activity from here.

Now look at terminal services. Find your connecting IP address still there.

Next open notpad.exe. 

## Find Actor Activity.

Analyze packet capture. 
See any base 64?  What was that? 


