# Creation

## Download and open the source code. (Sample Golang Ransomware - Not Ironcat)

1. Open Linux-Attack-Host in the guacamole console and run the following command:

`sudo git clone https://github.com/target111/go-crypt.git`

2. Make a new directory to hold the files you will be working on.

`mkdir notransomware`

3. Copy the test file from the go-crypt folder.

`cp 

3. Open *sample-ransom-code.go* with vscode
`code ./sample-ransom-code`

## Modify code for evasion

1. Open with `sudo nano` or if you want to follow along with your other favorite editor but nano is used for these instructions.
2. Press ctrl+3 then shift+3 to show line numbers.
3. Delete line 4 for the library ending in "machineid"
4. Delete line 158 starting with 'id' through 162 ending with "{".
5. Delete line 164 ""id": {id},"
6. Cursor down to line 189. Press end. Delte the characters "+ id" from the end of the string.
7. Press ctrl+x to save, and enter to save as main.go.
8. Build! `env GOOS=windows GOARCH=amd64 go build main.go`
9. Rename this version for your first test. `cp main.exe test-nochange-1.exe`

## Now let's get a little tricky by changing some of the words!


### Change function headers with the powerful ctrl+h command.

### Modify the ransom note

### Add command line argument requirement to execution in main function

!detection
