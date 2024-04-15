# AmigaAssign
A bash script to provide Amiga style assign command to Linux.

# What is this thing
This script adds an Amiga like ASSIGN command to Linux (using a bash script).
It allows paths to be referenced by a short, convenient name instead of the
full path string. It is like an alias for paths instead of commands.

A quick example. 

```bash
/home/user$ assign docroot /var/www/html
/home/user$ ls $docroot
index.html
/home/user$ cp website.html $docroot
/home/user$ chmod a+r $docroot/website.html
```

# History
A long time ago there was this computer call the Amiga. On the Amiga you
accessed different drives using a name followed by a colon (:). This is
similar to how Windows uses a letter followed by a colon (for example "C:").
On the Amiga drives where not limited to a single letter but used a name.
For example DF0: was the first disk drive.

The interesting thing was you could also make up new device names and set
them a path on another drive. So for example you could setup WORK: to be
on HD0:MyWork/Current. You could then access it using commands like 
"dir WORK:" or "copy file WORK:new_name". This was done with the assign
command.

This is something like it for the bash shell. It adds an assign command
that you "assign" a path name to a bash variable that can then be used
as a shortcut for that path. 

# How to install
Take the "bash_assigncmd" script and copy it to your home directory
under the name ".bash_assigncmd" (cp bash_assigncmd ~/.bash_assigncmd).
Next source this script from one of your bash startup scripts.
I suggest adding it to your .bashrc file (add the line
"source ~/.bash_assigncmd").

Run this command to add the line.
```bash
echo "source ~/.bash_assigncmd" >>~/.bashrc
```

# Usage
After you have installed the assign command and source it
(but typing ~/.bash_assigncmd or opening a new term window) you
can start using it.

```
Usage:
assign [OPTIONS] var [path]

Options:
   -d -- Delete assignment
```

# Adding a new assign
To add a new assignment the first argument is the new assignment name
you want to add. This is a bash variable and has the same rules that all
bash variables have. The second argument is the path you want to assign
to this variable.

So for example "assign test /home/user/test" is the same
as "export test=/home/user/test". The difference between exporting
the var and using the assign command is that the assign command
remembers the var between sessions (and is also available to all
future sessions).

## Add examples
Here are some examples of adding vars using assign.

Example                           | Use                                   | Expands to
--------------------------------- | ------------------------------------- | -----------------------------------------------
`assign c /`                      | `ls $c`                               | `ls /`
`assign doc /home/user/Documents` | `cp instructions.pdf $doc`            | `cp instructions.pdf /home/user/Documents`
`assign down ~/Downloads`         | `cat $down/AscIITable.txt`            | `cat ~/Downloads/AscIITable.txt`
`assign docroot /var/www/html`    | `chmod 777 $docroot/site1/index.html` | `chmod 777 /var/www/html/site1/index.html`

## Deleting an assignment
You delete an assignment using the -d option followed by the assignment to delete.  It will be freed from this point on.

## Showing existing assignments
If you type in assign without any arguments you will get a list of assignments with what they are set to.

**NOTE** When the assign's are listed they will also be reloaded.  This will allow you to update new assigns from another shell to your current one.

