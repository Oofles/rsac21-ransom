# Creation

## Download and open the source code. (Sample Golang Ransomware - Not Ironcat)

1. Open Linux-Attack-Host in the guacamole console and run the following command:

`sudo git clone https://github.com/target111/go-crypt.git`

2. Make a new directory to hold the files you will be working on.

`mkdir notransomware`

3. Copy the test file from the go-crypt folder.

`cp go-crypt/crypter/encrypt.go notransomware/main.go`

3. Open *** with vscode
`code ./sample-ransom-code`

## Modify code for evasion

1. Open with `sudo nano` or if you want to follow along with your other favorite editor but nano is used for these instructions.
2. Press ctrl+3 then shift+3 to show line numbers.
3. Delete line 4 for the library ending in "machineid"
4. Delete line 158 starting with 'id' through 162 ending with "{".
5. Delete line 164 ""id": {id},"
6. Cursor down to line 189. Press end. Delte the characters "+ id" from the end of the string.
7. Press ctrl+x to save, and enter to save as main.go.
8. Build! `env GOOS=windows GOARCH=386 build main.go`
9. Rename this version for your first test. `cp main.exe test1.exe`

## Now let's get a little tricky by changing some of the words!
1. Again open the source with `sudo nano main.go`
2. Press ctrl+3 and then shift+3 to show line numbers.
3. Press alt+r to open the replace option.
4. Type "encrypt" and press enter.
5. Then type "random" and press enter to replace the word encrypt with random.
6. Press A to do it for all cases.
7. Now cursor down to line 153 that should contain the function "rsa.randomOAEP".
8. Change this to "rsa.EncryptOAEP" and nothing else on the line. It is case sensitive.
9. Use ctrl+x to save.
10. Again build running `env GOOS=windows GOARCH=386 build main.go`

### Now you are just being mean

Add an argument requirement! 

1. Open the main.go file again with `sdo nano main.go`
2. Cursor down to the main function which should be around line 111 and look like "func main() {
3. Enter a new line below this line, right above "var files []string"
4. Insert the follow code in that new line.
```

```



### Add command line argument requirement to execution in main function

!detection
