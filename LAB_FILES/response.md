# Response

## Get ready! 
1. We don't want to run the fun for anyone else just yet. In the bottom left search bar type "windows security" and open the Windows Security App.
2. Click on Virus & threat protection.
3. Under Virust & threat protection settings click Manage settings.
4. Ensure that Automatic sample submission is turned off!
5. Also, turn off Cloud-delevered protection.
6. Close the windows defender settings, leaving real-time protection on.
7. Open wireshark by typing wireshark in the bottom left search bar and click the wireshark app, and begin capturing on the 'ethernet' interface.
8. Open an administrative command prompt and type "procmon" to open procmon, and accept the EULA.
9. You are ready!

## Launch!

The point here is to fast forward you to after the user clicked the wrong link, and then enaabled macros, and then thought it was totally normal when the doc was nonsense and office errored out and closed,...AND didn't tell you they used their admin account to local login everyday.  

1. Open the 'rsac-rasom' folder ond the windows desktop and browse into the "LAB_FILES" folder.
2. Inside this folder is a zip folder called "iai-rsac21", right click the extract the contents.
3. Open the extracted folder. Right click and copy the iai-rsac21.exe file.
4. Paste this file in the c:\ root directory.
5. Open an administrative command prompt (type cmd in the search bar and click the command prompt app)
6. Change directory the C:\ `cd c:\`
7. Run the malware! `iai-rsac21.exe`
9. Gotcha! No commandline arguments, no execution. Try again. `iai-rsac21.exe encrypt <password>`
10. Watch the exectution. 
11. Once it is complete stop the wireshark capture and stop the procmon capture.

## Now Respond As if you weren't the one who did it!
1.
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


