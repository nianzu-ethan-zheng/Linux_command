# Linxu_command
## Navigation
Check the current working directory
```
pwd  # stand for the Print Working Directory
```
Show the content of the current working path

```
ls [option][location]   # it's short for list
ls -l       # long information
```
Path is composed of two parts: relative path and absolute path
More on path:
```
~(tide)      # This is a shortcut for your home directory, 
               that is, /home/znz/a equal to ~\a

.(dot)       # This is a reference to the current directory
..(ddot)     # This is a reference to the parent directory
```

Change the path
```
cd [location] 
```

Shortcut of typing the path
```
Typing out these paths can be tedious, 
we can use the Tab Completion to help us. 
```

## Files
Everything is actually a file

Linux is an extensionless system
```
my image = my_image.png=my_image.txt=...
```

We can use the **file** to find out 
```
file [path]
```
Linux is case sensitive
```
test != tesT
```
Spaces in names
```
cd Holiday Photos # x
cd 'Holidy Photos' # use Quotes
cd Holidy\ Photos  # use the Espape Characters: backslash(\)
```
Hidden files or folders
```
use the .          # you can use the 'ls -a' to see the contents 
```

## Manual Pages
The manual pages are a set of pages that explain every command 
available in your system.

You can invoke the manual pages with the following command
```
man <command to look up>
```
It is possible to do a keyword search on the manual pages

This can be helpful if you're not quite sure of what command you may 
want to use but you know what you want to achieve.
```
man -k<search term>
```

## file manipulation

### making a directory
```
mkdir [options]<Directory>
```
If parent directories is needed, we can set the option as **-p**

the second one is **-v** which makes mkdir tell us what it is doing

### Remving a directory
```
rmdir [options]<Directory>       # the file must be empty
```

### Creating a blank file
```
touch [options]<Directory> 
```

###  Copying a file or Directory
```
cp [options] <source><destination>     # created a path if the 
                                         destination doesn't exist
```

use the **-r** to copy a directory to another place.

### Moving a file or directory
```
mv [options]<source><destination>
```
### rename files and directories
```
mv will be used to move a file or dirctory into a new directory
```

### remove a file (and non empty directories)
```
rm [options]<file> 
```

## Vi Text Editor

Two modes: Insert and Edit mode.
```
Edit - use keyboard to input "i"    ->  Insert
Insert - press "Esc" -> Edit
```


We will look at a tool to put content into files and edit that content
as well.

```
Edit mode:
ZZ        : save and exit
:w        : save file but don't exit
:wq       : again save file and exit
:q!       : discard all changes, since the last save, and exit
```

### view a file

```
cat <file>
```
```
Ctrl+ c          # universal signal for Cancel in linux
```

less allows you to move up and down within a file using the 
arrow keys. pressing b, 
you may go forward a whole page using **spacebar**

When you are done you can press q for quit
```
less <file>
```

### Navigating a file in Vi
```
Arrow keys - move the cursor around
j, k, h, l - move the cursor down, up, left and right (similar to the arrow keys)
^ (caret) - move cursor to beginning of current line
$ - move cursor to end of the current line
nG - move to the nth line (eg 5G moves to 5th line)
G - move to the last line
w - move to the beginning of the next word
nw - move forward n word (eg 2w moves two words forwards)
b - move to the beginning of the previous word
nb - move back n word
{ - move backward one paragraph
} - move forward one paragraph
```
### Deleting content
```
x - delete a single character
nx - delete n characters (eg 5x deletes five characters)
dd - delete the current line
dn - d followed by a movement command. Delete to where the movement command would have taken you. (eg d5w means delete 5 words)
```
### Undoing
Undoing changes in vi is fairly easy
```
u - Undo the last action (you may keep pressing u to keep undoing)
U (Note: capital) - Undo all changes to the current line
```

### several operations
```
copy and paste
search and replace
buffers
markers
ranges
settings
```

## Wildcards
Wildcards are a set of building blocks that allow you 
to create a pattern defining a set of files or directories.

```
* - represents zero or more characters
? - represents a single character
[] - represents a range of characters
```
```
[sv]   : s or  v
[0-9]  : 0~9
[^a-k] : any character except a-k
```

## Permissions
Linux permissions dictate 3 you may do with a file: read,write and execute

```
r read - you may view the contents of the file.
w write - you may change the contents of the file.
x execute - you may execute or run the file if it is a program or script.
```
We can define 3 sets of people for whom we may specify permissions
```
owner - a single person who owns the file. (typically the person who created the file but ownership may be granted to some one else by certain users)
group - every file belongs to a single group.
others - everyone else who is not in the group or the owner.
```
### view permissions
```
ls -l [path]
 ```

- rwx r-- --x 1 harry users 2.7K Jan 4 07:32 
```
first character identifies the file type: dash(-) means it is normal file
                                          d means it is a directory
the following 3 character represent the permissions for owner: dash means the absence of permission
--------------3------------------------------------ for the group
--------------3------------------------------------ for the others
                                 
```
### change permissions
```
chmod   [permissions] [path]               # it stands for change file mode which is a bit of a mouthfull

Who are we changing the permission for? 
[ugoa] - user (or owner), group, others, all

Are we granting or revoking the permission 
- indicated with either a plus ( + ) or minus ( - )

Which permission are we setting? 
- read ( r ), write ( w ) or execute ( x )
```
```
ls -l frog.png
-rwxr----x 1 harry users 2.7K Jan 4 07:32 frog.png
chmod g+x frog.png
ls -l frog.png
-rwxr-x--x 1 harry users 2.7K Jan 4 07:32 frog.png
chmod u-w frog.png
ls -l frog.png
-r-xr-x--x 1 harry users 2.7K Jan 4 07:32 frog.png

```

### Setting permission shorthand

```
Octal	Binary
0	0 0 0
1	0 0 1
2	0 1 0
3	0 1 1
4	1 0 0
5	1 0 1
6	1 1 0
7	1 1 1
```

```
ls -l frog.png
-rw-r----x 1 harry users 2.7K Jan 4 07:32 frog.png
chmod 751 frog.png
ls -l frog.png
-rwxr-x--x 1 harry users 2.7K Jan 4 07:32 frog.png
chmod 240 frog.png
ls -l frog.png
--w-r----- 1 harry users 2.7K Jan 4 07:32 frog.png

```

Permissions for Directories
```
r - you have the ability to read the contents of the directory (ie do an ls)
w - you have the ability to write into the directory (ie create files and directories)
x - you have the ability to enter that directory (ie cd)
```

### the root user

On a linux system there are only 2 people usually who may change the permissions of a file or directory
, the owner of the file or directory and the root user.

### basic security

##  Filters
A fitler, in context of the linux command line, is a program that accept textual data and then
transform it in particular way.
### View
```
cat                                      # look the whole article
head [-number of lines to print] [path]  # it is a program that prints the first n lines of the article
tail                                     # the last n lines of the article
```
### sort and numberate
```
sort                                     # it will sort alphabetically but there are many
                                           options available to modify the sorting mechanism
nl                                       # it stands for numbering lines
```
### word count
```
wc                                       # it stands for word count

wc by default will give a count fo all 3 but using command line options we may limit it to
just we are after
-l         # number of lines
-w         # number of words
-m         # number of characters
```
### get column
```
cut [-options] [path]                   # cut is a nice program to use if your content is 
                                          seperated into fields(columns) and you only want 
                                          certain fields

-f          # field
-d          # seperator
```

### replace  and remove tediousness
```
sed <expression> [path]                   # stream editor; it effectively allows us to do a search
                                          and replace on our data

expression: 
s                    # substitude
/search
/replace/
g                    # global
```
```
uniq                                      # it stands for unique and its job is to remove duplicate
                                            lines in data
                                            Its limitation is those lines must be adjacent
```

### reverse view
```
tac                                       # tac is actually cat in reverse; Given data it will
                                            print the last line first
```

## Grep and Regular Expressions
The basic behaviour of egrep is that it will print the entire line for every line which contains a string of characters matching the given pattern. This is important to note, we are not searching for a word but a string of characters.
```
egrep [command line options]<pattern>[path]   
```

```
. (dot) - a single character.
? - the preceding character matches 0 or 1 times only.
* - the preceding character matches 0 or more times.
+ - the preceding character matches 1 or more times.
{n} - the preceding character matches exactly n times.
{n,m} - the preceding character matches at least n times and not more than m times.
[agd] - the character is one of those included within the square brackets.
[^agd] - the character is not one of those included within the square brackets.
[c-f] - the dash within the square brackets operates as a range. In this case it means either the letters c, d, e or f.
() - allows us to group several characters to behave as one.
| (pipe symbol) - the logical OR operation.
^ - matches the beginning of the line.
$ - matches the end of the line.
```
## Piping and Redirection

Every program we run on the command line automatically has three data streams connected 
to it

```
STDIN(0)            # standard input 
STDOUT(1)           # standard output 
STDERR(2)           # standard error
``` 
Piping and redirection is the means by which we may connect these streams between programs
and files to direct data in interesting and useful ways.

### redirecting to a file

Normally we will get our output on the screen, which is convenient most of the time. but sometime we
may wish to save it into a file to keep as a record.
```
>              # the greater operator indicates to saved in a file insteed of printed to the screen
                 New file | old file: cleared and rewrite
>>             # double greater than operator, old file: the new data to be appended to the file 
```
### redirecting from a file
```
<              # we use the less than operator, read data from file and feed it into program 
```

### redirecting stderr
```
2>             # with a number
```

### piping
So far we've dealt with sending data to and from files, 

now we'll take a look at a mechanism for
sending data from one program to another. It's called piping
```
|                                  # operator
```

```
ls
barry.txt bob example.png firstfile foo1 myoutput video.mpeg
ls | head -3
barry.txt
bob
example.png
```
```
ls | head -3 | tail -1 > myoutput
cat myoutput
example.png
```

## process management
tweak the running fo the system to better suit our need.

a program is a series of instructions that tell the computer what to do.
When we run a program, those instruction are copied into memory and space is allocated to variables
and other stuff required to manage its execution.






