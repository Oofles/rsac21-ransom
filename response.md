# Response

## Get ready! 
Open process explorer
Open wireshark and start capturing
Disable defender and real time protections

## Login to the Windows Victim Box and Detonate Ransomware

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
3. Use the [windows_fundamentals.md}(windows fundamentals) resource to look for various indicators of activity.