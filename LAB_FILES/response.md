# Response

## Get ready! 
1. We don't want to run the fun for anyone else just yet. In the bottom left search bar type "windows security" and open the Windows Security App.
2. Click on Virus & threat protection.
3. Under Virus & threat protection settings click Manage settings.
4. Ensure that Automatic sample submission is turned off!
5. Also, turn off Cloud-delevered protection.
6. Close the windows defender settings, leaving real-time protection on.
7. Open wireshark by typing wireshark in the bottom left search bar and click the wireshark app.
8. In the top menu choose Capture>Options.
9. Now click the output tab.
10. Next to the file input, click Browse.
11. Choose the c:\ and input the filename of "investigation" and click save. 
12. Now click start capture to capturing on the 'ethernet' interface.
13. Open an administrative command prompt and type "procmon" to open procmon, and accept the EULA.
14. You are ready!

## Launch!

The point here is to fast forward you to after the user clicked the wrong link, and then enaabled macros, and then thought it was totally normal when the doc was nonsense and office errored out and closed,...AND didn't tell you they used their admin account to local login everyday.  

1. Open the 'rsac-rasom' folder ond the windows desktop and browse into the "LAB_FILES" folder.
2. Inside this folder is a zip folder called "iai-rsac21", right click the extract the contents.
3. Open the extracted folder. Right click and copy the iai-rsac21.exe file.
4. Paste this file in the c:\ root directory. So that you see c:\
5. Open an administrative command prompt (type cmd in the search bar and click the command prompt app)
6. Change directory the C:\ `cd c:\`
7. Run the malware! `iai-rsac21.exe`
9. Gotcha! No commandline arguments, no execution. Try again. `iai-rsac21.exe encrypt <password>`
10. Watch the exectution. 
11. Once it is complete stop the wireshark capture and stop the procmon capture.

## Now Respond As if you weren't the one who did it!

1. Use the [Windows Fundamentals](windows_fundamentals.md) resource to look for various indicators of activity.

## Files, Files,Files
Don't close the the cmd prompt.
ctrl+c. 
Use the history command to find the command line arguments used.
```history```

Get as much information from the ransomnote as possible>
What is the size and file type. When was it created, and last modified or access and who owns it?
`powershell get-file`


## Orientate

1. Okay, there is note. Don't click it yet!
2. Some links don't work. You go to open windows explorer or search for an app and it the links fail.
3. If you can't use windows+r or are not comfortable....the recycle bin is a good option to open up a file explorer.
4. From here you can browse to C:\Windows\System32\cmd.exe and open the command line or other tools as you normally would.

## Log analysis, All my friends...
Event view shows all logs cleared.  So you can't get the command line activity from here.
Before you do anyting else, let's check some logs.  Normally you would pull the logs with a forensic script, but in this lab environment just take a look.
1. Launch event viewer. `eventvwr`
2. Suprise they are all cleared. But go check out the following logs. Microsoft>Windows>TerminalServices-*  As you look around you will see information logged from your still active RDP session. If you disconnected this is where a disconnection event would occur revealing the remote IP.
3. Exit event viewer.
4. In the administrative command prompt make a investigation directory and move the firewall logs from system32 into that directory.
```
mkdir c:\investigation
cd c:\investigation
xcopy c:\Windows\System32\LogFiles\Firewall\pfirewall.log .
notepad pfirewall.log
```
5. Inspect the windows firewall log. Notice anything about this log? It isn't cleared, and it wasn't encrypted. This is generally the case because actors do not want to encrypt system32 and break the machine. We will regroup with a demonstration of how usefull this traffic can be.

## Analyze the packet capture. And track down that pesky activity.

1. Save the packet capture to the c:\.
2. Open the packet capture and type 'http' in the display filter.
3. Notice the DNS request right before the HTTP request?
4. Right click on one of the http packets going to 34.x.x.x and choose follow>http
5. What do you see? What is the base64 info? In your devices browser go to cyberchef.io.
6. You will find when using the base64 decode that this is actually the key being sent. This is not a realistic in the sense of it being a password you can use to decrypt the files. However, it is realistic in the value add that can come from capturing the initial conversations that can be gathered from live packet capture.

Netstat to find activity.
Now track that to the pid.
Now track the pid to the process information and find the file reponsible. Look at the time stampe. Maybe other files were modified here too?

## Track Down the Scorched Earth Protocol Network Actions

1. In the administrative command prompt(not powershell) run `netstat -anob 1 | findstr 80`
2. Find the PID of the network activity going to 35. and run `tasklist /FI "PID EQ <instert pid>"
3. The results show a supicious process making that network connection. Swap to powershell `powershell`
4. Get more information from that process  `get-process -id "<pid>" | select *`
5. In the path you will see it's location inside C:\Windows\SysWOW64\ . That is one clue. Time to dig deeper.
6. Use this command to find the command line used to launch the process. `get-ciminstance Win32_Process |?{$_.ProcessID -eq <pid>}|select *` In the output find the command line output. You will see it being ran with 3 arguments, likley changing the behavior of the executable again!.
7. Now you know for sure that files have been planted from the original execution. 

## What did they do!
One more way you can quickly pull information together in a ransomware attack is to look at file time lines. Ransomware happens, you are called in and the user generally doesn't do too much. Not to mention you have tracked activity back to some specific folders. How do you find the rest?

1. In an administrative command prompt, enter powershell. `powershell`
2. Get the time of the incident from the ransomnote. There are other places and times to look at such as the logs clearing, but for this instance use the note. `$target = (get-childitem -path c:\Users\Administrator\Desktop\<ransomnotefilename>).CreationTime`
3. Now create an start and end time window. 
```
$starttime = $target.AddMinutes(-5)
$endtime = $target.AddMinutes(5)`
```
5. And use that as the target window to find files created in some select locations including the already identified SysWow64 location.
```
get-childitem c:\windows\ | ?{$_.CreationTime -gt $target} | Select Name
get-childitem c:\windows\syswow64 | ?{$_.CreationTime -gt $target} | Select Name
get-childitem c:\windows\system32 | ?{$_.CreationTime -gt $starttime -and $_CreationTime -lt $target} | Select Name
```
> You can do this with a small enough window with the 'recurse' option on the entire c:\Windows folder, but you will still need to sort through some noise.
6. Now you should have identified quiet a few .bat files. Go inspect the to find out what is going on, and figure out how to shut down the Scorched Earth Protocol.

**All of the activity from this exectuable will be revealed at the end of the lab, and uploaded to this github.**


 


