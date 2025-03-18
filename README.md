# LEDIP
## a text editor for the KIM-1

There was this small entry on hansotten.nl about a line editor for the KIM-1 called Ledip. Not much infos were given, except some scanned pages of Dr.Dobbs journal issue 29. including the manual and sourcecode Sadly the scans were, well, not very usable. 8 and B and D and 0 were indistinguishable. Litterally. The author of the program, Kiumi Akingbehin, meanwhile Professor at the Michigan University, was so kind to send me another scan. Slightly better, but still far away from being readable.

But I gave it a try anyway and needed like three days to type this little program in and compile it. There were lots of tons of Typos by myself, but with the help of hjm and Hans Otten and their eagle eyes, all errors were found and now this 43 year old piece of software history is revived again, ready to play with.

![LEDIP in action](https://github.com/netzherpes/LEDIP/raw/main/ledip2.jpg)

Instructions: Load the papertape into your KIM-1, clone or the fabulous iOS Emulator "VirtualKIM".<br>
Start the Program at place 2000 (mem expansion required).<br> 
It will now ask for a starting adress, where the text should be stored. Any free space is possible, for example $3000. This Value is very important later and wil be stored in the Zero Page as MbegL $d5 and MbegH $d6 .<br>
The End adresses (MendL $d3 and MendH $d4) are updated with every line you type, modify, delete, insert. A lot of Memory shuffeling is going on, when you insert a line in between two existing lines of text: Copy the upfollowing lines exact the ammount of bytes upwards as the inserted text is long and change the end address... Brainfck if you look at the sources. Amazing and perfect RAM saving when memory was rare.

The folowing commands are accepted:

    Add text with a 4 digit line number: *0010* Hello World!
    *LIST* lists the text with line numbers
    *TEXT* lists the text without line numbers
    *FILE* gives you all needed memory locations to save the text: Zero pages, the program itself and the textarea.
    *EXIT* ... guess.
    *CLEAR* delete everything

Warmstart is $203C ! - Important if you load some files uo again

Thanks to: Kiumi Akingbehin, HJM and Hans Otten for their help,

Have fun, stay childish,<br> Yours Webdoktor

**UPDATE:** let's say you have an existing text on your pc and want to convert it in a way, that LEDIP can process it. The syntax in linux or cygwin is as follows:

    nl -nrz -w4 -s  text_in.txt > text_out.txt

(important are the 2 spaces after -s)

Pro Tipp: Good textfiles can be found [here](http://textfiles.com/sex/EROTICA/)

:P
UPDATE II
WARMSTART IS AT $203C

## MECB version for use with 65c02 monitor

Modified to use TASM assembler for compatibility with 65c02 monitor
This version is built to run in ram at 0x2000 with i/o patched to use 65c02 monitor functions.
Note: an additional call to character out is made after character inputfor screen echo.
Note: page zero addresses are default, may conflict with BASIC - to check
A version is being built to reside in rom as part of the monitor.


Built under DOSBox-X with build.bat

```
tass /c /lledip.lbl ledip.asm ledip.bin ledip.lst
```

Binary image converted to s-records with commad:
```
srec_cat ledip.bin -binary -offset 0x1ffe -output ledip.hex -Intel -address-length=2
```

Load in 65c02 monitor using U command and xmodem transfer of file ledip.hex, execute at 0x2000


