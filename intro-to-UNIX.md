I am writing up a short UNIX shell tutorial to prepare you for QIIME2 analysis. There are roughly 10-12 UNIX commands you will need to practice to run various plugins for QIIME2.

First recommendation, use a Text Editor (like [TextWrangler, BBEdit](https://www.barebones.com/products/textwrangler/))
This is useful because you can record code, scripts without losing any of the syntax. 

For example the single quote `'` and double quote `"` will be different in Word or Powerpoint.

## Prompt

First think you'll notice is your prompt $ the dollar sign, called the `prompt`. The gray area identifies the terminal entry for the following examples:
```
$
```
The string of characters before the dollar sign `$` are your username and machine name. The `~` tilde will indicate your working directory. The QIIME Workshop AWS will have two lines with the server directory relative path:
```
<ENTER-DIRECTORY-PATH>
$
```
## 1. Print Working Directory `pwd`

The first command to learn is `print your current working directory`. Type `pwd` and press enter.
```
pwd
```
You will get and output line:
```
<insert pwd>
```
The prompt sign `$` will return, that means the computer is ready for another input. `pwd` is very useful if you are lost in your filesystem.

## 2. List `ls`

Now that we know where we are, what is __in__ our current directory. Let's type `ls` which is list:
```
$ ls
```
The `ls` command shows a variety of listing options. For example adding `-lh` will output the format differently:

```
$ ls -lh
```
Compare the two printed outputs. `-lh` is long format and human readable. The bytes size will differ to make it easy to see the file size. You will have a `working` directory, also known as folder. 

## 3. Make new directory `mkdir`

We will need to keep our files and directories in order. Let's make a new directory using the command `mkdir`. This command requires the usage of `mkdir <new-directory-name>`. Type:
```
$ mkdir 2018 12 12
```
We quickly find out, spacing is _IMPORTANT_. We receive an error. What's happening?

`mkdir` command is making three directories: `2018` `12` and `12`, but the last one won't be made because you already wrote `12`. 

Type the `ls` command to view the contents in your current directory:
```
$ ls
```
You will see the two directories `2018`and `12`.

To understand what is happening, use the `--help` option:
```
$ mkdir --help
mkdir: illegal option -- -
usage: mkdir [-pv] [-m mode] directory ...
```
The `...` means a space betweeen a directory name denotes another directory. We had `2018` space `12`, resulting in two directories.

Or run the `man` command to a command and a BSD General Commands Manual will pop-up:
```
$ man mkdir
```
This will list a more _interactive_ option for understand the command. Type `q` to exit.

## 4. Move `mv`

Let's rename the directory `2018` to `2018-12-12`. This requires the `mv` command, there is no rename command. The syntax is:
```
mv <directory-to-rename> <new-directory-name>
```
We will type:
```
$ mv 2018-12-12 
```
To check if we renamed 2018, type:
```
$ ls
```
## 5. Remove directory `rmdir`
Since we have an unnecessary `12` directory, let's remove! The syntax for the command `rmdir` is:
```
$ rmdir <directory-name>
```
Type:
```
$ rmdir 12
```
To check if you removed it, type:
```
$ ls
```
Do you see a directory named `12`?

## 6. Change Directory `cd`

`cd` will allow you to move around into different directories. Now that we created a new directory called "2018-12-12", let's move into that directory using the `cd` change directory command. The syntax to run `cd` is:
```
$ cd <directory-name>
```
Type in:
```
$ cd 20
```
And then hit **TAB**. This will auto-fill the rest of the available files.

Now print your working directory.
```
$ pwd
```
Do you see you are now in `username/2018-12-12`. 

**CHALLENGE**

Let's make a new directory called 'example', change into that 'example' directory and print your working directory.

```
$ mkdir example
$ cd example
$ pwd
```
What do you see?

Let's go back to the `2018-12-12` directory.
```
$ cd ..
```
`cd ..` is going up one directory. Type:

```
$ pwd
```
Finally, let's go back home just using:
```
$ cd
```

## 7. Nano - open a text editor

We can use an interactive program called `nano` to generate a simple `.txt` file. Type:
```
$ nano
```
A new screen will pop-up. Type in a few lines.
```
future me will thank past me
for information about my analysis
leave hints for this workflow
```
Press `CTRL-O` which will [save file, filename to write]. Enter:
```
example.txt
```
Press enter. Then `CTRL-X` to exit editor. Type:
```
$ ls
```
To edit the file again, type:
```
$ nano example.txt
```
## 8. Revisiting `mv`

Where are you? Use:
```
$ pwd
```
Let's move the `example.txt` into the `2018-12-12/` directory. The command `mv` syntax is:
```
$ mv <source-to-move> <target-directory>
```
So we will need to put our source file and target directory in. Use **TAB** to autocomplete:

```
$ mv example.txt 2018-12-12
```
Type `ls` to see if you moved the file from your current working directory:
```
$ ls
```

## 9. Revising remove `rm` 

There is another way to remove both files and directories. This is permanent. Use the flag `-i` to check if you want to remove the file before you do this. The first will ask to examine the available files to remove.

Remove a single file, we just made example.txt and we don't want it anymore. It is located in the `2018-12-12` directory:
```
$ ls 2018-12-12
$ rm -i 2018-12-12/example.txt 
remove example.txt? y
$ ls
```
Remove a directory, this requires a recursive `-r` option because we need to remove the contents within the directory. The `-i` option will ask to examine which files in the directory to remove and then confirm the removal. Type in `y` or `yes` to confirm.
```
$ rm -r -i 2018-12-12/
examine files in directory 2018-12-12/? y
remove 2018-12-12/? y
$ ls
```
## 10. `wget` 
To download a file from a URL, we use the command `wget`. The syntax is:

```
wget -O [URL]
```
We will download the `sample-metadata.tsv` file from my test account:
```
$ wget -O "sample-metadata.tsv" "https://workshop-server.qiime2.org/focused-sloth/sample-metadata.tsv"
```
## 11. Copy `cp`

We can copy a file to another directory using the syntax:
```
cp -i <source-file> <target-file> [-i flag will ask approval]
cp -i <source-file> <target-directory>
cp -i <source-file> . [. is current directory] 
```
Let's copy the `test.tsv"` file to 
```
$ mkdir back-up
$ cp -i sample-metadata.tsv back-up
$ ls back-up
```
## 12. Viewing `less`

```
$ less back-up/sample-metadata.tsv 
```
Using ENTER, scroll down the file. To EXIT, press `q`.

## 13. Print top ten lines `head`

```
$ head back-up/sample-metadata.tsv 

```

## 14. Print last ten lines `tail`

Use ARROW-UP to re-enter the whole last command. Then CRTL-A to go to the beginning of string. Delete `head` and enter `tail`:

```
$ tail back-up/sample-metadata.tsv 

```

## 15. Redirect `>` - print to a file

```
$ head -n 10 back-up/sample-metadata.tsv > top-of-file.txt
$ ls
$ less top-of-file.txt
```
You should see the output file is in your current working directory and not your `back-up/` directory.

## 16. qiime commands

QIIME is installed on the AWS. We can "see" available qiime plugins by typing:

```
$ qiime
```
qiime will subcommands listed, including plugin commands (e.g.
feature-table, diversity) and built-in commands (e.g. info, tools).

You can discover what plugins you currently have installed, as well as
other information about your QIIME deployment, by running qiime info:
```
$ qiime info
```

## We hope you feel comfortable with this refresher. All of these commands take practice. Below are more tips for shortcuts and important keys.

## Short-cut keys:
```
tab "autocomplete"
arrow up "last command"
arrow down "current command"
CTRL-A "move to the beginning of the string"
CTRL-E "move to the end of the string"
```

## Important keys:
```
~ tilde
\ backslash
` backtick
' single quote
" double quote
* asterisk
_ underscore
{} curly braces
[] square brackets
() parentheses
# hash mark
+ plus sign
- minus sign (hyphen or dash)
. dot
! exclamation mark
> redirect
| pipe
```
