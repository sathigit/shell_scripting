Wellcome to shell_scripting tutorils
Shell Scripting

A Shell provides you with an interface to the Unix system. It gathers input from you and executes programs based on that input. When a program finishes executing, it displays that program's output.
Shell is an environment in which we can run our commands, programs, and shell scripts. There are different flavors of a shell, just as there are different flavors of operating systems. Each flavor of shell has its own set of recognized commands and functions.
Shell Prompt
The prompt, $, which is called the command prompt, is issued by the shell. While the prompt is displayed, you can type a command.
Shell reads your input after you press Enter. It determines the command you want executed by looking at the first word of your input. A word is an unbroken set of characters. Spaces and tabs separate words.
Following is a simple example of the date command, which displays the current date and time −
$date
Thu Jun 25 08:30:19 MST 2009
You can customize your command prompt using the environment variable PS1 explained in the Environment tutorial.
Shell Types
In Unix, there are two major types of shells −
Bourne shell − If you are using a Bourne-type shell, the $ character is the default prompt.
C shell − If you are using a C-type shell, the % character is the default prompt.
The Bourne Shell has the following subcategories −
Bourne shell (sh)
Korn shell (ksh)
Bourne Again shell (bash)
POSIX shell (sh)
The different C-type shells follow −
C shell (csh)
TENEX/TOPS C shell (tcsh)
The original Unix shell was written in the mid-1970s by Stephen R. Bourne while he was at the AT&T Bell Labs in New Jersey.
Bourne shell was the first shell to appear on Unix systems, thus it is referred to as "the shell".
Bourne shell is usually installed as /bin/sh on most versions of Unix. For this reason, it is the shell of choice for writing scripts that can be used on different versions of Unix.
In this chapter, we are going to cover most of the Shell concepts that are based on the Borne Shell.
Shell Scripts
The basic concept of a shell script is a list of commands, which are listed in the order of execution. A good shell script will have comments, preceded by # sign, describing the steps.

Assume we create a test.sh script. Note all the scripts would have the .sh extension. Before you add anything else to your script, you need to alert the system that a shell script is being started. This is done using the shebang construct. For example −
#!/bin/sh
This tells the system that the commands that follow are to be executed by the Bourne shell. It's called a shebang because the # symbol is called a hash, and the ! symbol is called a bang.


Default umask Value
The user file-creation mode mask (umask) is use to determine the file permission for newly created files. It can be used to control the default file permission for new files. It is a four-digit octal number. A umask can be set or expressed using:
Symbolic values
Octal values
Procedure To Setup Default umask
You can setup umask in /etc/bashrc or /etc/profile file for all users. By default most Linux distro set it to 0022 (022) or 0002 (002). Open /etc/profile or ~/.bashrc file, enter:
# vi /etc/profile
OR
$ vi ~/.bashrc
Append/modify following line to setup a new umask:
umask 022
Save and close the file. Changes will take effect after next login. All UNIX users can override the system umask defaults in their /etc/profile file, ~/.profile (Korn / Bourne shell) ~/.cshrc file (C shells), ~/.bash_profile (Bash shell) or ~/.login file (defines the user’s environment at login).
Explain Octal umask Mode 022 And 002
As I said earlier, if the default settings are not changed, files are created with the access mode 666 and directories with 777. In this example:
1. The default umask 002 used for normal user. With this mask default directory permissions are 775 and default file permissions are 664.
2. The default umask for the root user is 022 result into default directory permissions are 755 and default file permissions are 644.
3. For directories, the base permissions are (rwxrwxrwx) 0777 and for files they are 0666 (rw-rw-rw).
In short,
1. A umask of 022 allows only you to write data, but anyone can read data.
2. A umask of 077 is good for a completely private system. No other user can read or write your data if umask is set to 077.
3. A umask of 002 is good when you share data with other users in the same group. Members of your group can create and modify data files; those outside your group can read data file, but cannot modify it. Set your umask to 007 to completely exclude users who are not group members.
But, How Do I Calculate umasks?
The octal umasks are calculated via the bitwise AND of the unary complement of the argument using bitwise NOT. The octal notations are as follows:
Octal value : Permission
0 : read, write and execute
1 : read and write
2 : read and execute
3 : read only
4 : write and execute
5 : write only
6 : execute only
7 : no permissions
Now, you can use above table to calculate file permission. For example, if umask is set to 077, the permission can be calculated as follows:
Bit
Targeted at
File permission
0
Owner
read, write and execute
7
Group
No permissions
7
Others
No permissions
To set the umask 077 type the following command at shell prompt:
$ umask 077
$ mkdir dir1
$ touch file
$ ls -ld dir1 file
Sample outputs:
drwx------ 2 vivek vivek 4096 2011-03-04 02:05 dir1
-rw------- 1 vivek vivek    0 2011-03-04 02:05 file
TASK: CALCULATING THE FINAL PERMISSION FOR FILES
You can simply subtract the umask from the base permissions to determine the final permission for file as follows:
666 – 022 = 644
File base permissions : 666
umask value : 022
subtract to get permissions of new file (666-022) : 644 (rw-r–r–)
TASK: CALCULATING THE FINAL PERMISSION FOR DIRECTORIES
You can simply subtract the umask from the base permissions to determine the final permission for directory as follows:
777 – 022 = 755
Directory base permissions : 777
umask value : 022
Subtract to get permissions of new directory (777-022) : 755 (rwxr-xr-x)
How Do I Set umask Using Symbolic Values?
The following symbolic values are used:
1. r : read
2. w : write
3. x : execute
4. u : User ownership (user who owns the file)
5. g : group ownership (the permissions granted to other users who are members of the file’s group)
6. o : other ownership (the permissions granted to users that are in neither of the two preceding categories)


difference between umask and chmod


umask sets the default permissions for your files when they are created, 
while chmod is used to change the file permissions after they are created. 
The value of umask masks with the default creation mode as implemented by 
the OS which is 777 for directories and 666 for files in linux. 

So if you have a umask of 022 then you can quickly calculate the permissions 
of new directories by (777 - 022) = 755 
and for files (666 - 022) = 644. 

data duplicator
The dd command stands for “data duplicator” and used for copying and converting data. It is very powerful low level utility of Linux which can do much more like;
• Backup and restore the entire hard disk or partition.
• Backup of MBR (Master Boot Record)
• It can copy and convert magnetic tape format, convert between ASCII and EBCDIC formats, swap bytes          and can also convert lower case to upper case.
• It can also be used by Linux kernel make files to make boot images.
Only superuser can run this command because you can face a big data loss due to it’s improper usage, so you should be very careful while working with this utility. At that moment data loss can convert the dd utility as a “data destroyer” for you. That’s why it is recommended that beginners should not use this command on a production machine until they get familiarity on this. You must make sure that target location must have sufficient space while running this command.
SYNTAX OF DD COMMAND
Before we start with some practical work we need to talk about it’s syntax.
dd if=<source file name> of=<target file name> [Options]
We normally do not explain about syntax but this command syntax require some explanation. The syntax is totally different when compared to many Linux commands we know. In this syntax dd is followed by two things
if=<source> –This is a source from where you want to copy data and ‘if’ stands for input-file.
of=<destination> –This is a source from where you want to write/paste data and ‘of’ stands for output-file.
[options] –These options include, how fast data should be written, what format etc.
Input(source file name) and Output(target file name) in syntax are disks, partitions, files and devices to which you want to write and read data from. There are many options which we will discuss in examples.
LEARN LINUX DD COMMAND WITH EXAMPLES
Example 1: Clone one hard disk to another hard disk. This is useful when we are building many machines with same configuration. We no need to install OS on all the machines. Just install OS and required software on machine then clone with below example.
 
dd if=/dev/sda of=/dev/sdb
Example 2: We can take backup of a partition/complete HDD for future restoration.
Related concept:   Access Linux From Windows Through Virtual Network Computing(VNC)
Backing up a partition to a file(to my home directory as hdadisk.img)
dd if =/dev/sda2 of=~/hdadisk.img
Restoring this image file in to other machine
dd if=hdadisk.img of=/dev/sdb3
Example 3: Do you feel hdadisk.img is bit big? Use gzip or bzip2 to compress when creating image.
dd if =/dev/sda2 | bzip2 hdadisk.img.bz2
Example 4: Do you know dd command can be used as file copier as well? Yes, if you don’t have cp command use dd command to copy a file from one location to other.
dd if=/home/imran/abc.txt of=/mnt/abc.txt
Ok, that is fine for basic use of dd command. But the beauty of dd command lies in advanced usages like wiping of disks, complete wiping of disks, MBR backups etc.
ADVANCED USAGE OF LINUX DD COMMAND
From here you should be careful when using this command and you should first try these commands on a test machine before getting familiarity.
Example 5: Wipe/delete content of a disk so that it will be empty for some one to use it.
dd if=/dev/zero of=/dev/sdb
This will wipe out your second hard disk and every bit is written with zero. you may be interested in learning /dev/null and /dev/zero files which do similar stuff but there is a bit of difference.
HOW WRITING OF A FILE  ON HARD DISK WITH DATA HAPPEN?
Normally what ever you write on to a disk at the block level it will write combination of zeros and ones. Hope you know this and what we are doing here is that we are just writing zeros which will clear all 1’s from the hard disk. This eventually makes your disk empty.
Example 6: What to hide your ass by deleting your personal data. Many people think if we do rm -rf /<your data> will do the needful. But we can recover those deletion by using disk recovery tools like Photorec or some forensic tools. But if you want some not to recover your data you have to write random data on your partition where you data resides.
dd if=/dev/random of=/dev/sdb
Do above command multiple times so that it is real hard to recover data. If I am in your place, I will write below shell script to do that.
for i in {1..10};do dd if=/dev/random of=/dev/sdb;done
This will execute dd command 10 times in a row one after the other.
Related concept:   How To Find Growing Files In Linux?
Example 7: We can create virtual file system with dd command which can be used as swap. To know more about you should know on how to create virtual swap space in Linux.
dd if=/dev/zero of=/swapfile bs=1024 count=200000
where bs stands for block size and count is nothing but number of such blocks used to crate this swap file.
Make sure you use block sizes in multiples of 1024 bytes which is equal to 1KB. Ff you do not specify block size, dd use a default block size of 512 bytes. Below conventions will work for block sizes.
N and BYTES may be followed by the following multiplicative suffixes: c =1, w =2, b =512,
kB =1000, K =1024, 
Mb =1000*1000, MB=1024*1024, 
Gb =1000*1000*1000, GB =1024*1024*1024, 
and so on for T, P, E, Z, Y.
Example 8: We can even create ISO files from a CD-ROM or DVD-ROM using dd command.
dd if=/dev/dvd of=/opt/my_linux_image.iso
or with more
dd if=/dev/sr0 of=/home/$user/mycd_image.iso bs=2048 conv=sync
Some other examples:
dd if=/dev/sda1 of=/dev/sdb1 bs=4096 conv=noerror,sync
This will make clone of one partition sda1 to other sdb1 partition, also used sync option to synchronize the partition
dd if=/dev/sdx of=/dev/sdy bs=64k conv=noerror,sync
This will clone the entire drive, including MBR, all partitions and data where noerrr instructs dd to ignore all read errors while continuing operations. The snyc data offsets stay in sync And bs=sets block size which is set to 64k.
Example 9: We can even check disk quota using dd command by creating huge files which eats up HDD in no time.
dd if=/dev/zero of=/usr/disk-img/disk-quota.ext3 count=40960 
This will create 20MB file (disk image) at said path.

cut

The cut command in UNIX is a command line utility for cutting sections from each line of files and writing the result to standard output.
How to cut by byte position
To cut out a section of a line by specifying a byte position use the -b option.
echo 'baz' | cut -b 2
a
echo 'baz' | cut -b 1-2
ba
echo 'baz' | cut -b 1,3
bz
How to cut by character
To cut by character use the -c option. This selects the characters given to the -coption. This can be a list of comma separated numbers, a range of numbers or a single number.
Where your input stream is character based -c can be a better option than selecting by bytes as often characters are more than one byte.
In the following example character ‘♣’ is three bytes. By using the -c option the character can be correctly selected along with any other characters that are of interest.
echo '♣foobar' | cut -c 1,6
♣a
echo '♣foobar' | cut -c 1-3
♣fo
How to cut based on a delimiter
To cut using a delimiter use the -d option. This is normally used in conjunction with the -f option to specify the field that should be cut.
In the following example a CSV file exists and is saved as names.csv.
John,Smith,34,London
Arthur,Evans,21,Newport
George,Jones,32,Truro
The delimiter can be set to a comma with -d ','. cut can then pull out the fields of interest with the -f flag. In the following example the first field is cut.
cut -d ',' -f 1 names.csv
John
Arthur  
George
Multiple fields can be cut by passing a comma separated list.
cut -d ',' -f 1,4 names.csv
John,London
Arthur,Newport
George,Truro
How to cut by complement pattern
To cut by complement us the --complement option. Note this option is not available on the BSD version of cut. The --complement option selects the inverse of the options passed to sort.
In the following example the -c option is used to select the first character. Because the --complement option is also passed to cut the second and third characters are cut.
echo 'foo' | cut --complement -c 1
oo
How to modify the output delimiter
To modify the output delimiter use the --output-delimiter option. Note that this option is not available on the BSD version of cut. In the following example a semi-colon is converted to a space and the first, third and fourth fields are selected

echo 'how;now;brown;cow' | cut -d ';' -f 1,3,4 --output-delimiter=' '
how brown cow

man
man is the system's manual viewer; it can be used to display manual pages, scroll up and down, search for occurrences of specific text, and other useful functions.
 banner 
The Unix banner program outputs a large ASCII art version of the text that is supplied to it as its program arguments. One use of the command is to create highly visible separator pages for print jobs.
Each argument is truncated at 10 characters and printed on a "line" of its own. To print multiple words on a single line, they must therefore be passed as a single argument, which is done from the shell by escaping or quoting the words as appropriate.

compress
compress is a Unix shell compression program based on the LZW compression algorithm.[1] Compared to more modern compression utilities such as gzip and bzip2, compress performs faster and with less memory usage, at the cost of a significantly lower compression ratio.
The uncompress utility will restore files to their original state after they have been compressed using the compress utility. If no files are specified, the standard input will be uncompressed to the standard output.
Files compressed by compress are typically given the extension ".Z"

gzip and gunzip
use gzip and gunzip commands with examples. Gzip(GNU zip) is a compress tool which is available in most of the Linux/Unix based operating systems. Until recent years gzip and bzip2 are most commonly used data compression tools in Linux/Unix. Though gzip compress ratios are not good when compared to bzip2 but it is popular among masses. Gzip software uses Lempel-Ziv coding (LZ77)algorithm for compressing data. In this post we will see how to install, use as well as tips about gzip command.
13 Zip and Unzip command examples in Linux/Unix
How to install gzip and gunzip(GNU unzip) command in Linux?
On Redhat, Centos and Fedora based machines
yum -y install gzip gunzip
On Ubuntu and Debian based machines

apt-get install gzip gunzip
Learn gzip command with examples
Example1: Syntax for zipping a file with gzip command.
Syntax:
gzip file1 file2 file3
Example:
surendra@linuxnix:~/test/test$ ls
2  3  4   dump.doc  file1  test.sh
surendra@linuxnix:~/test/test$ gzip dump.doc file1 test.sh 
surendra@linuxnix:~/test/test$ ls
2  3  4  dump.doc.gz  file1.gz  test.sh.gz
Note: Above gzip command will create files dump.doc.gz, file1.gz and test.sh.gz respectively by replacing original files.


kill Command
Purpose
Sends a signal to running processes.
Syntax
To Send Signal to Processes
kill [  -s { SignalName | SignalNumber } ] ProcessID ...
kill [  - SignalName |  - SignalNumber ] ProcessID ...
To List Signal Names
kill -l [ ExitStatus ]
Examples
1. To stop a given process, enter the following command:
kill 1095
This stops process 1095 by sending it the default SIGTERM signal. Note that process 1095 might not actually stop if it has made special arrangements to ignore or override the SIGTERM signal.
2. To stop several processes that ignore the default signal, enter the following command:
kill -kill 2098 1569
This sends signal 9, the SIGKILL signal, to processes 2098 and 1569. The SIGKILL signal is a special signal that normally cannot be ignored or overridden.
3. To stop all of your processes and log yourself off, enter the following command:
kill -kill 0
This sends signal 9, the SIGKILL signal, to all processes that have a process group ID equal to the senders process group ID. Because the shell cannot ignore the SIGKILL signal, this command also stops the login shell and logs you off.
4. To stop all processes that you own, enter the following command:
kill -9 -1
This command sends signal 9, the SIGKILL signal, to all processes that are owned by the effective user, even those processes that are started at other workstations and that belong to other process groups. If a listing that you requested is being printed, it is also stopped.
5. To send a different signal code to a process, enter the following command:
kill  -USR1  1103
The name of the kill command is misleading because many signals, including SIGUSR1, do not stop processes. The action that is taken on SIGUSR1 is defined by the particular application you are running.
Note: To send signal 15, the SIGTERM signal with this form of the kill command, you must explicitly specify -15 or TERM.


comm
Compare two sorted files line-by-line.
Description
Compare sorted files FILE1 and FILE2 line-by-line.
With no options, comm produces three-column output. Column one contains lines unique to FILE1, column two contains lines unique to FILE2, and column three contains lines common to both files. Each of these columns can be suppressed individually with options.
comm syntax
comm [OPTION]... FILE1 FILE2
Options
-1
suppress column 1 (lines unique to FILE1)
-2
suppress column 2 (lines unique to FILE2)
-3
suppress column 3 (lines that appear in both files)
--check-order
check that the input is correctly sorted, even if all input lines are pairable
--nocheck-order
do not check that the input is correctly sorted
--output-delimiter=STR
separate columns with string STR
--help
display a help message, and exit.
--version
output version information, and exit.
Examples
Let's say you have two text files, recipe.txt and shopping-list.txt.
recipe.txt contains these lines:
All-Purpose Flour
Baking Soda
Bread
Brown Sugar
Chocolate Chips
Eggs
Milk
Salt
Vanilla Extract
White Sugar
And shopping-list.txt contains these lines:
All-Purpose Flour
Bread
Brown Sugar
Chicken Salad
Chocolate Chips
Eggs
Milk
Onions
Pickles
Potato Chips
Soda Pop
Tomatoes
White Sugar
As you can see, the two files are different, but many of the lines are the same. Not all of the recipe ingredients are on the shopping list, and not everything on the shopping list is part of the recipe.
If we run the comm command on the two files, it will read both files and give us three columns of output:
comm recipe.txt shopping-list.txt
All-Purpose Flour
Baking Soda
                Bread
                Brown Sugar
        Chicken Salad
                Chocolate Chips
                Eggs
                Milk
        Onions
        Pickles
        Potato Chips
Salt
        Soda Pop
        Tomatoes
Vanilla Extract
                White Sugar
Here, each line of output has either zero, one, or two tabs at the beginning, separating the output into three columns:
1. The first column (zero tabs) is lines that only appear in the first file.
2. The second column (one tab) is lines that only appear in the second file.
3. The third column (two tabs) is lines that appear in both files.
(The columns overlap visually because in this case, our terminal prints a tab as eight spaces. It might look different on your screen.)
Next, let's look at how we can bring our separated data into a spreadsheet.
Creating a CSV File For Spreadsheets
One useful way to use comm is to output to a CSV file, which can then be read by a spreadsheet program. CSV files are just text files that use a certain character, usually a comma, tab, or semicolon, to delimit data in a way that can be read as a spreadsheet. By convention, CSV filenames have the extension .csv.
For instance, let's run the same command, but this time let's redirect the output to a file called output.csv by using the > operator:
comm recipe.txt shopping-list.txt > output.csv
This time there is no output on the screen. Instead, output is sent to a file called output.csv. To check that it worked correctly, we can cat the contents of output.csv:
cat output.csv
All-Purpose Flour
Baking Soda
                Bread
                Brown Sugar
        Chicken Salad
                Chocolate Chips
                Eggs
                Milk
        Onions
        Pickles
        Potato Chips
Salt
        Soda Pop
        Tomatoes
Vanilla Extract
                White Sugar

tee
Reads from standard input, and writes to standard output and to files.
Description
The tee command is named after the T-splitter in plumbing, which splits water into two directions and is shaped like an uppercase T.
tee copies data from standard input to each FILE, and also to standard output. In effect, tee duplicates its input, routing it to multiple outputs at once.
tee syntax
tee [OPTION]... [FILE]...
Options
-a, --append
Append to the given FILEs. Do not overwrite.
-i, --ignore-interrupts
Ignore interrupt signals.
--help
Display a help message, and exit.
--version
Display version information, and exit.
If a FILE is specified as a dash ("-"), tee writes again to standard output.
tee examples
ls -1 *.txt | wc -l | tee count.txt
In the above example, the ls command lists all files in the current directory that have the file name extension .txt, one file per line; this output is piped to wc, which counts the lines and outputs the number; this output is piped to tee, which writes the output to the terminal, and writes the same information to the file count.txt. If count.txt already exists, it is overwritten.


mesg
The md5sum command computes and checks the MD5 message digest.
Description
Print or check MD5 (128-bit) checksums. With no FILE, or when FILE is -, read standard input.
Note: The MD5 algorithm should not be used any more for security related purposes. Instead, better use an SHA-2 algorithm, implemented in the programs sha224sum, sha256sum, sha384sum, and sha512sum.
md5sum syntax
 md5sum [OPTION]... [FILE]...
Options
-b, --binary
Read in binary mode.
-c, --check
Read MD5 sums from the FILEs and check them.
--tag
Create a BSD-style checksum.
-t, --text
Read in text mode (default).
Note: There is no difference between binary and text mode option on GNU system.
The following four options are useful only when verifying checksums:
--quiet
Don't print OK for each successfully verified file.
--status
Don't output anything, status code shows success.
--strict
Exit non-zero for improperly formatted checksum lines.
-w, --warn
Warn about improperly formatted checksum lines.
--help
Display this help and exit.
--version
Output version information and exit.
The sums are computed as described in RFC 1321. When checking, the input should be a former output of this program. The default mode is to print a line with checksum, a character indicating input mode ('*' for binary, space for text), and name for each FILE.
md5sum examples
md5sum sample.txt
Running the above command would give the md5 checksum of the example.iso file in the current directory. Below is an example of how the output may appear with the full md5 checksum followed by the file name.
d41d8cd98f00b204e9800998ecf8427e sample.txt


What is an MD5 checksum?
An MD5 checksum is a 32-character hexadecimal number that is computed on a file. 
The MD5 checksum or digest or hash has been widely used in the software world to provide some assurance that a transferred file has arrived intact. For example, file servers often provide a pre-computed MD5, so that a user can compare the checksum of the downloaded file to it
If two files have the same MD5 checksum value, then there is a high probability that the two files are the same. 
After downloading an MQ software installation package, you can compute the MD5 checksum on the installation file.

The MD5 checksum or MD5 hash is a more secure alternative to the checksums obtained from the "sum" or "cksum" commands. The sum and cksum commands are file integrity utilities that are based on a weak cyclic redundancy check mechanism (32-bit wide), and this mechanism is prone to high collision rates.
Answer
For illustration purposes, a file from one machine was copied as file "binary.file" into a network shared drive, then the following tests were performed to obtain the MD5 checksum on different platforms.
In all cases the MD5 checksum for this file is: 0c4627e70d168f7f78257e6dd01fdb60

LINUX: md5sum fileName

In Linux, the md5sum utility can be used:
aemtux1:/ % md5sum binary.file
0c4627e70d168f7f78257e6dd01fdb60 binary.file

This utility is provided by the following rpm package (the package name is the key element, because the version number depends on your Linux installation)
% rpm -qf /usr/bin/md5sum
coreutils-5.2.1-23.13




ln
ln creates links between files.
Description
ln creates a link to file TARGET with the name LINKNAME. If LINKNAME is omitted, a link to TARGET is created in the current directory, using the name of TARGET as the LINKNAME.
ln creates hard links by default, or symbolic links if the -s (--symbolic) option is specified. When creating hard links, each TARGET must exist.
What Is A Link?
Before we discuss the ln command, let's first discuss the link command, as well as what a link is and how it relates to files as we know them.
A link is an entry in your file system which connects a file name to the actual bytes of data on the disk. More than one file name can "link" to the same data. Here's an example. Let's create a file named file1.txt:
echo "This is a file." > file1.txt
This command echoes the string "This is a file". Normally this would echo to our terminal, but the >operator redirects the string's text to a file, in this case file1.txt. We can check that it worked by using cat to display the contents of the file:
cat file1.txt
This is a file.
When this file was created, the operating system wrote the bytes to a location on the disk and also linked that data to a file name, file1.txt so that we can refer to the file in commands and arguments. If you rename the file, the contents of the file are not altered; only the information that points to it. The file name and the file's data are two separate entities.
Here's an illustration of the file name and the data to help you visualize it:

Using The link Command
What the link command does is allow us to manually create a link to file data that already exists. So, let's use link to create our own link to the file data we just created. In essence, we'll create another file name for the data that already exists.
Let's call our new link file2.txt. How do we create it?
The general form of the link command is: "link file_name linkname". Our first argument is the name of the file whose data we're linking to; the second argument is the name of the new link we're creating.
link file1.txt file2.txt
Now both file1.txt and file2.txt point to the same data on the disk:
cat file1.txt
This is a file.
cat file2.txt
This is a file.
The important thing to realize is that we did not make a copy of this data. Both file names point to the same bytes of data on the disk. Here's an illustration to help you visualize it:

If we change the contents of the data pointed to by either one of these files, the other file's contents are changed as well. Let's append a line to one of them using the >> operator:
echo "It points to data on the disk." >> file1.txt
Now let's look at the contents of file1.txt:
cat file1.txt
This is a file.
It points to data on the disk.
... and now let's look at the second file, the one we created with the link command:
cat file2.txt
This is a file.
It points to data on the disk.
Both files show the change because they share the same data on the disk. Changes to the data of either one of these files will change the contents of the other.
But what if we delete one of the files? Will both files be deleted?
No. If we delete one of the files, we're deleting one of the links to the data. Because we created another link manually, we still have a pointer to that data; we still have a way, at the user-level, to access the data we put in there. So if we use the rm command to remove our first file:
rm file1.txt
...it no longer exists as a file with that name:
cat file1.txt
cat: file1.txt: No such file or directory
...but the link to the data we manually created still exists, and still points to the data:
cat file2.txt
This is a file.
It points to data on the disk.
As you can see, the data stays on the disk even after the "file" (which is actually just a link to the data) is removed. We can still access that data as long as there is a link to it. This is important to know when you're removing files — "removing" a file just makes the data inaccessible by unlink-ing it. The data still exists on the storage media, somewhere, inaccessible to the system, and that space on disk is marked as being available for future use.
The type of link we've been working with here is sometimes called a "hard" link. A hard link and the data it links to must always exist on the same filesystem; you can't, for instance, create a hard link on one partition to file data stored on another partition. You also can't create a hard link to a directory. Only symbolic links may link to a directory; we'll get to that in a moment.
The Difference Between ln And link
So what about ln? That's why we're here, right?
ln, by default, creates a hard link just like link does. So this ln command:
ln file1.txt file2.txt
...is the same as the following link command:
link file1.txt file2.txt
...because both commands create a hard link named file2.txt which links to the data of file1.txt.
However, we can also use ln to create symbolic links with the -s option. So the command:
ln -s file1.txt file2.txt
Will create a symbolic link to file1.txt named file2.txt. In contrast to our hard link example, here's an illustration to help you visualize our symbolic link:

About Symbolic Links
Symbolic links, sometimes called "soft" links, are different than "hard" links. Instead of linking to the data of a file, they link to another link. So in the example above, file2.txt points to the link file1.txt, which in turn points to the data of the file.
This has several potential benefits. For one thing, symbolic links (also called "symlinks" for short) can link to directories. Also, symbolic links can cross file system boundaries, so a symbolic link to data on one drive or partition can exist on another drive or partition.
You should also be aware that, unlike hard links, removing the file (or directory) that a symlink points to will break the link. So if we create file1.txt:
echo "This is a file." > file1.txt
...and create a symbolic link to it:
ln -s file1.txt file2.txt
...we can cat either one of these to see the contents:
cat file1.txt
This is a file.
cat file2.txt
This is a file.
...but if we remove file1.txt:
rm file1.txt
...we can no longer access the data it contained with our symlink:
cat file2.txt
cat: file2.txt: No such file or directory
This error message might be confusing at first, because file2.txt still exists in your directory. It's a broken symlink, however — a symbolic link which points to something that no longer exists. The operating system tries to follow the symlink to the file that's supposed to be there (file1.txt), but finds nothing, and so it returns the error message.
While hard links are an essential component of how the operating system works, symbolic links are generally more of a convenience. You can use them to refer, in any way you'd like, to information already on the disk somewhere else.
Creating Symlinks To Directories
To create a symbolic link to a directory, specify the directory name as the target. For instance, let's say we have a directory named documents, which contains one file, named file.txt.
Let's create a symbolic link to documents named dox. This command will do the trick:
ln -s documents/ dox
We now have a symlink named dox which we can refer to as if it is the directory documents. For instance, if we use ls to list the contents of the directory, and then to list the contents of the symlinked directory, they will both show the same file:
ls documents
file.txt
ls dox
file.txt
When we work in the directory dox now, we will actually be working in documents, but we will see the word dox instead of documents in all pathnames.
Symbolic links are a useful way to make shortcuts to long, complicated pathnames. For instance, this command:
ln -s documents/work/budgets/Engineering/2014/April aprbudge
...will save us a lot of typing; now, instead of changing directory with the following command:
cd documents/work/budgets/Engineering/2014/April
...we can do this, instead:
cd aprbudge
Normally, you remove directories (once they're empty) with the rmdir command. But our symbolic link is not actually a directory: it's a file that points to a directory. So to remove our symlink, we just use the rm command:
rm aprbudge
This will remove the symlink, but the original directory and all its files are not affected.
ln syntax
ln [OPTION]... TARGET [...] [LINKNAME [...]]
Options
Here are the options that can be passed to the ln command.
--backup[=CONTROL]
Use this option to additionally create a backup of each existing destination file. The style of backup is optionally defined by the value of CONTROL. See belowfor more information.
-b
This functions like --backup, but you cannot specify the CONTROL; the default style (simple) is used.
-d, -F, --directory
This option allows the superuser to attempt to hard link directories (although it will probably fail due to system restrictions, even for the superuser).
-f, --force
If the destination file or files already exist, overwrite them.
-i, --interactive
Prompt the user before overwriting destination files.
-L, --logical
Dereference TARGETs that are symbolic links. In other words, if you are trying to create a link (or a symlink) to a symlink, link to what it links to, not to the symlink itself..
-n, --no-dereference
Treat LINKNAME as a normal file if it is a symbolic link to a directory.
-P, --physical
Make hard links directly to symbolic links, rather than dereferencing them.
-r, --relative
Create symbolic links relative to link location.
-s, --symbolic
Make symbolic links instead of hard links.
-S, --suffix=SUFFIX
Use the file suffix SUFFIX rather than the default suffix "~".
-t, --target-directory=DIRECTORY
Specify the DIRECTORY in which to create the links.
-T, --no-target-directory
Always treat LINKNAME as a normal file.
-v, --verbose
Operate verbosely; print the name of each linked file.
--help
Display a help message, and exit.
--version
Display version information, and exit.
About The --backup Option
When using the --backup (or -b) option, the default file suffix for backups is '~'. You can change this, however, using the --suffix option or setting the SIMPLE_BACKUP_SUFFIX environment variable.
The CONTROL argument to the --backup option specifies the version control method. Alternatively, it can be specified by setting the VERSION_CONTROL environment variable. Here are the values to use for either one:
none, off
Never make backups (even if --backup is given).
numbered, t
Make numbered backups.
existing, nil
Numbered if numbered backups exist, simple otherwise.
simple, never
Always make simple backups.
If you use -b instead of --backup, the CONTROL method is always simple.
If you specify the -s option (which symlinks), ln ignores the -L and -P options. Otherwise (if you are making hard links), the last option specified controls behavior when a TARGET is a symbolic link. The default is to act as if -P was specified.
ln examples
ln public_html/myfile1.txt
Create a hard link to the file public_html/myfile1.txt in the current directory.
ln -s public_html/myfile1.txt
Create a symbolic link to the file public_html/myfile1.txt in the current directory.
ln -s public_html/ webstuff
Create a symbolic link to the directory public_html named webstuff.
ln -s -b file1.txt file2.txt
Creates a symbolic link to the file file1.txt named file2.txt. If file2.txt already exists, it is renamed to file2.txt~ before the new file2.txt symlink is created.



Dpkg

dpkg queries, installs, removes, and maintains Debian software packages and their dependencies.
Description
The primary and more user-friendly front-end for dpkg is aptitude. dpkg itself is controlled entirely via command line parameters, which consist of exactly one action and zero or more options. The action-parameter tells dpkg what to do and options control the behavior of the action in some way.
dpkg can also be used as a front-end to dpkg-deb and dpkg-query. The list of supported actions is below (in the "Actions" section). If any such action is encountered dpkg just runs dpkg-deb or dpkg-query with the parameters given to it, but no specific options are currently passed to them, to use any such option the back-ends need to be called directly.
dpkg syntax
dpkg [option...] action

dpkg examples
dpkg -l '*vi*'
List installed packages related to the editor vi.
dpkg --print-avail elvis vim | less
View the entries of the packages elvis and vim as listed in /var/lib/dpkg/available.
less /var/lib/dpkg/available
Manually view the list of available software packages.
dpkg -r elvis
Remove the installed package elvis.
dpkg -i vim_4.5-3.deb
Install the package contained in the file vim_4.5-3.deb.
dpkg --get-selections >myselections
Make a local copy of the package selection states.


Dmesg

dmesg examines or controls the kernel ring buffer.
The kernel ring buffer is a data structure that records messages related to the operation of the kernel. A ring buffer is a special kind of buffer that is always a constant size, removing the oldest messages when new messages come in.
dmesg syntax
dmesg [options]
Options
-C, --clear
Clear the ring buffer.
-c, --read-clear
Clear the ring buffer contents after printing.
-D, --console-off
Disable printing messages to the console.
-d, --show-delta
Display the timestamp and time delta spent between messages. If used with --notime then only the time delta without the timestamp is printed.
-E, --console-on
Enable printing messages to the console.
-f, --facility list
Restrict output to defined (comma separated) list of facilities. For all supported facilities see --help output.
-h, --help
Print a help text and exit.
-k, --kernel
Print kernel messages.
-l, --level list
Restrict output to defined (comma separated) list of levels. For all supported levels see --help output.
-n, --console-level level
Set the level at which messages are logged to the console. The level is a level number or abbreviation of the level name. For example, -n 1 or -n alert prevents all messages except emergency (panic) messages from appearing on the console. All levels of messages are still written to /proc/kmsg, so syslogd(8) can still be used to control exactly where kernel messages appear. When the -n option is used, dmesg will not print or clear the kernel ring buffer. For all supported levels see --help output.
-r, --raw
Print the raw message buffer, i.e., don't strip the log level prefixes.
-s, --buffer-size size
Use a buffer of size to query the kernel ring buffer. This is 16392 by default. If you have set the kernel buffer to be larger than the default then this option can be used to view the entire buffer.
-T, --ctime
Print human readable timestamps. The timestamp could be inaccurate; The time source used for the logs is not updated after system SUSPEND/RESUME.
-t, --notime
Don't print kernel's timestamps.
-u, --userspace
Print userspace messages.
-V, --version
Output version information and exit.
-x, --decode
Decode facility and level (priority) number to human readable prefixes.
The default action of dmesg is to read all messages from kernel ring buffer.
dmesg examples
dmesg > kernel_msgs.txt
Output all kernel messages currently in the ring buffer to a file called kernel_msgs.txt.
dmesg | grep -i memory
Display only those kernel messages which relate to memory usage.

Useradd

useradd creates a new user or sets the default information for new users.
Description
useradd is a low-level utility for adding users to a system. In general, the more friendly addusershould be used instead.
Your operating system may come with a slightly different version of useradd; check your documentation before using it to create new accounts. This documentation refers to some options frequently used on Debian-based variants of Linux, but is representative of useradd's general use.
When invoked without the -D option, the useradd command creates a new user account using the values specified on the command line plus the default values from the system. Depending on command line options, the useradd command will update system files and may also create the new user's home directory and copy initial files.
By default, a group will also be created for the new user (see the -g, -N, -U options, and the USERGROUPS_ENAB variable, below).
useradd syntax
useradd [options] LOGIN
useradd -D
useradd -D [options]
Options
-c, --comment COMMENT
COMMENT can be any text string. It is generally a short description of the login, and is currently used as the field for the user's full name.
-d, --home HOME_DIR
The new user will be created using HOME_DIR as the value for the user's login directory. The default is to append the LOGIN name to BASE_DIR and use that as the login directory name. The directory HOME_DIR does not have to exist but will not be created if it is missing.
-D, --defaults
Set new default values. See the section on Changing New User Default Values, below.
-e, --expiredate EXPIRE_DATE
The date on which the user account will be disabled. The date is specified in the format YYYY-MM-DD.

If not specified, useradd will use the default expiry date specified by the EXPIRE variable in /etc/default/useradd, or an empty string (no expiry) by default.
-f, --inactive INACTIVE
The number of days after a password expires until the account is permanently disabled. A value of 0 disables the account as soon as the password has expired, and a value of -1 disables the feature.

If not specified, useradd will use the default inactivity period specified by the INACTIVE variable in /etc/default/useradd, or -1by default.
-g, --gid GROUP
The group name or number of the user's initial login group. The group name must exist. A group number must refer to an already existing group.

If not specified, the behavior of useradd will depend on the USERGROUPS_ENAB variable in /etc/login.defs. If this variable is set to yes (or -U/--user-group is specified on the command line), a group will be created for the user, with the same name as her loginname. If the variable is set to no (or -N/--no-user-group is specified on the command line), useradd will set the primary group of the new user to the value specified by the GROUP variable in /etc/default/useradd, or 100 by default.
-G, --groups GROUP1[,GROUP2,...[,GROUPN]]]
A list of supplementary groups which the user is also a member of. Each group is separated from the next by a comma, with no intervening whitespace. The groups are subject to the same restrictions as the group given with the -g option. The default is for the user to belong only to the initial group.
-h, --help
Display a help message, and exit.
-k, --skel SKEL_DIR
SKEL_DIR is the skeleton directory, which contains files and directories to be copied in the user's home directory, when the home directory is created by useradd.

This option is only valid if the -m (or --create-home) option is specified.

If this option is not set, the skeleton directory is defined by the SKEL variable in /etc/default/useradd or, by default, /etc/skel.

If possible, the ACL and extended attributes are copied.
-K, --key KEY=VALUE
Overrides /etc/login.defs defaults (UID_MIN, UID_MAX, UMASK, PASS_MAX_DAYS and others).

Example: -K PASS_MAX_DAYS=-1 can be used when creating system account to turn off password aging, even though system account has no password at all. Multiple -K options can be specified, for example: -K UID_MIN=100 -K UID_MAX=499
-l, --no-log-init
Do not add the user to the lastlog and faillog databases.

By default, the user's entries in the lastlog and faillog databases are resetted to avoid reusing the entry from a previously deleted user.

For the compatibility with previous versions of useradd, the -Ooption is also supported for this purpose.
-m, --create-home
Create the user's home directory if it does not exist. The files and directories contained in the skeleton directory (which can be defined with the -k option) will be copied to the home directory.

By default, if this option is not specified and CREATE_HOME is not enabled, no home directories are created.
-M
Do no create the user's home directory, even if the system wide setting from /etc/login.defs (CREATE_HOME) is set to yes.
-N, --no-user-group
Do not create a group with the same name as the user, but add the user to the group specified by the -g option or by the GROUPvariable in /etc/default/useradd.

The default behavior (if the -g, -N, and -U options are not specified) is defined by the USERGROUPS_ENAB variable in /etc/login.defs.
-o, --non-unique
Allow the creation of a user account with a duplicate (non-unique) UID.

This option is only valid in combination with the -u option.
-p, --password PASSWORD
The encrypted password, as returned by crypt. The default is to disable the password.

Note: This option is not recommended because the password (or encrypted password) will be visible by users listing the processes (for example, with the ps command).

You should make sure the password respects the system's password policy.
-r, --system
Create a system account.

System users will be created with no aging information in /etc/shadow, and their numeric identifiers are chosen in the SYS_UID_MIN-SYS_UID_MAX range, defined in /etc/login.defs, instead of UID_MIN-UID_MAX (and their GID counterparts for the creation of groups).

Note that useradd will not create a home directory for such an user, regardless of the default setting in /etc/login.defs(CREATE_HOME). You have to specify the -m options if you want a home directory for a system account to be created.
-R, --root CHROOT_DIR
Apply changes in the CHROOT_DIR directory and use the configuration files from the CHROOT_DIR directory.
-s, --shell SHELL
The name of the user's login shell. The default is to leave this field blank, which causes the system to select the default login shell specified by the SHELL variable in /etc/default/useradd, or an empty string by default.
-u, --uid UID
The numerical value of the user's ID. This value must be unique, unless the -o option is used. The value must be non-negative. The default is to use the smallest ID value greater than or equal to UID_MIN and greater than every other user.

See also the -r option and the UID_MAX description.
-U, --user-group
Create a group with the same name as the user, and add the user to this group.

The default behavior (if the -g, -N, and -U options are not specified) is defined by the USERGROUPS_ENAB variable in /etc/login.defs.
-Z, --selinux-user SEUSER
The SELinux user for the user's login. The default is to leave this field blank, which causes the system to select the default SELinux user.
Changing New User Default Values
When invoked with only the -D option, useradd will display the current default values. When invoked with -D plus other options, useradd will update the default values for the specified options.
Valid default-changing options are:
-b, --base-dir BASE_DIR
The path prefix for a new user's home directory. The user's name will be affixed to the end of BASE_DIR to form the new user's home directory name, if the -d option is not used when creating a new account.

This option sets the HOME variable in /etc/default/useradd.
-e, --expiredate EXPIRE_DATE
The date on which the user account is disabled.

This option sets the EXPIRE variable in /etc/default/useradd.
-f, --inactive INACTIVE
The number of days after a password has expired before the account will be disabled.

This option sets the INACTIVE variable in /etc/default/useradd.
-g, --gid GROUP
The group name or ID for a new user's initial group (when the -N/--no-user-group is used or when the USERGROUPS_ENAB variable is set to no in /etc/login.defs). The named group must exist, and a numerical group ID must have an existing entry.

This option sets the GROUP variable in /etc/default/useradd.
-s, --shell SHELL
The name of a new user's login shell.

This option sets the SHELL variable in /etc/default/useradd.
Notes
The system administrator is responsible for placing the default user files in the /etc/skel/ directory (or any other skeleton directory specified in /etc/default/useradd or on the command line).
Caveats
You may not add a user to a NIS or LDAP group. This must be performed on the corresponding server.
Similarly, if the username already exists in an external user database such as NIS or LDAP, useraddwill deny the user account creation request.
It is usually recommended to only use usernames that begin with a lower case letter or an underscore, followed by lower case letters, digits, underscores, or dashes. They can end with a dollar sign. The regular expression which describes a valid user name is:
[a-z_][a-z0-9_-]*[$]?
The only constraints are that usernames must neither start with a dash ('-') nor plus ('+') nor tilde ('~') nor contain a colon (':'), a comma (','), or a whitespace (space: ' ', end of line: '\n', tab: '\t', etc.). Note that using a slash ('/') may break the default algorithm for the definition of the user's home directory.
Usernames may only be up to 32 characters long.
Configuration
The following configuration variables in /etc/login.defs change the behavior of this tool:
name
type
description
CREATE_HOME
boolean
Indicate if a home directory should be created by default for new users.

This setting does not apply to system users, and can be overridden on the command line.
GID_MAX, GID_MIN
number
Range of group IDs used for the creation of regular groups by useradd, groupadd, or newusers.

The default value for GID_MIN is 1000; the default for GID_MAX is 60000.
MAIL_DIR
string
The mail spool directory. This is needed to manipulate the mailbox when its corresponding user account is modified or deleted. If not specified, a compile-time default is used.
MAIL_FILE
string
Defines the location of the users mail spool files relatively to their home directory.
The MAIL_DIR and MAIL_FILE variables are used by useradd, usermod, and userdel to create, move, or delete the user's mail spool.
MAX_MEMBERS_PER_GROUP
number
Maximum members per group entry. When the maximum is reached, a new group entry (line) is started in /etc/group (with the same name, same password, and same group ID).

The default value is 0, meaning that there are no limits in the number of members in a group.

This feature (split group) can help to limit the length of lines in the group file. This is useful to make sure that lines for NIS groups are not larger than 1024 characters.

If you need to enforce such limit, you can use 25.

Note: split groups may not be supported by all tools, even advanced tools like the Shadow toolsuite. You should not use this variable unless you really need it.
PASS_MAX_DAYS
number
The maximum number of days a password may be used. If the password is older than this, a password change will be forced. If not specified, -1 will be assumed (which disables the restriction).
PASS_MIN_DAYS
number
The minimum number of days allowed between password changes. Any password changes attempted sooner than this will be rejected. If not specified, -1 will be assumed (which disables the restriction).
PASS_WARN_AGE
number
The number of days warning given before a password expires. A zero means warning is given only upon the day of expiration, a negative value means no warning is given. If not specified, no warning will be provided.
SYS_GID_MAX, SYS_GID_MIN
number
Range of group IDs used for the creation of system groups by useradd, groupadd, or newusers.

The default value for SYS_GID_MIN is 101; the default value for SYS_GID_MAX is GID_MIN minus 1.
SYS_UID_MAX, SYS_UID_MIN
number
Range of user IDs used for the creation of system users by useraddor newusers.

The default value for SYS_UID_MIN is 101; the default value of SYS_UID_MAX is UID_MIN minus 1.
UID_MAX, UID_MIN
number
Range of user IDs used for the creation of regular users by useraddor newusers.

The default value for UID_MIN (resp. UID_MAX) is 1000 (resp. 60000).
UMASK
number
The file mode creation mask is initialized to this value. If not specified, the mask will be initialized to 022. useradd and newusers use this mask to set the mode of the home directory they create. It is also used by pam_umask as the default umask value.
USERGROUPS_ENAB
boolean
If set to yes, userdel will remove the user's group if it contains no more members, and useradd will create by default a group with the name of the user.
Files
/etc/passwd
User account information.
/etc/shadow
Secure user account information.
/etc/group
Group account information.
/etc/gshadow
Secure group account information.
/etc/default/useradd
Default values for account creation.
/etc/skel/
Directory containing default files.
/etc/login.defs
Shadow password suite configuration.
Exit Status
useradd exits with the following status, depending on what occurred:
0
Everything was completed successfully.
1
Couldn't update the password file.
2
The syntax of the command was invalid.
3
One or more options were given an invalid argument.
4
User ID is already in use, and -o was not specified.
6
Specified group doesn't exist.
9
Username already in use.
10
Couldn't update the group file.
12
Couldn't create the home directory.
14
Couldn't update SE Linux user mapping.
useradd examples
Note: For these commands to work you must have root privileges.
useradd -D
Displays the defaults for new users. Output resembles the following:
GROUP=1001
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
CREATE_MAIL_SPOOL=no
useradd newperson
Creates newperson as a new user. Once the new user has been added, you would need to use the passwd command to assign a password to the account.
Once a user has been created, you can modify any of the user settings, such as the user's home directory, using the usermod command.

Bzip2

Bzip2 is used to compress a file in order to reduce disk space, it is quite popular in Linux and UNIX operating systems for this reason. Bzip2 has been around since the late 1990s and is still widely used today. It may be preferable over gzip as it can produce smaller compressed files, at the cost of additional memory and processing time.
We are going to cover 10 examples of bzip2 here, showing you common tasks that can be completed and just how easy it is to use.
Requirements
Before starting you will need to have the bzip2 package installed, this may already be installed by default, however you can install it now if required.
RHEL:
yum install bzip2
Debian:
apt-get install bzip2
Example Bzip2 Commands
1. Compress a single file
This will compress file.txt and create file.txt.bz2, note that this will remove the original file.txt file.
bzip2 file.txt
2. Compress multiple files at once
This will compress all files specified in the command, note again that this will remove the original files specified by turning file1.txt, file2.txt and file3.txt into file1.txt.bz2, file2.txt.bz2 and file3.txt.bz2
bzip2 file1.txt file2.txt file3.txt
To instead compress all files within a directory, see example 7 below.
3. Compress a single file and keep the original
You can instead keep the original file and create a compressed copy.
bzip2 -c file.txt > file.txt.bz
The -c flag outputs the compressed copy of file.txt to stdout, this is then sent to file.txt.bz2, keeping the original file.txt file in place.
The version of bzip2 that I am testing with, 1.0.6, which is currently the latest available as of this writing also has the -k option which keeps the original file, so alternatively you could also run the below command to get the same result.
bzip2 -k file.txt
4. Decompress a bzip2 compressed file
To reverse the compression process and get the original file back that you have compressed, you can use the bzip2 command itself or bunzip2 which is also part of the bzip2 package.
bzip2 -d file.txt.bz2
OR
bunzip2 file.txt.bz2
Both of these commands will produce the same result, decompressing file.txt.bz2 to file.txt, removing the compressed file.txt.bz2 file.
Similar to example 3, it is possible to decompress a file and keep the original .bz2 file as below.
bunzip2 -c file.txt.bz2 > file.txt
OR
bunzip2 -k file.txt.bz2
5. List compression information
With the -v or --verbose flag we can see useful information regarding the compression ratio of a file, which shows us how much disk space our compression is saving. Additional ‘v’ flags can be added for more in depth information.
[root@centos ~]# bzip2 -v linux-3.18.19.tar
  linux-3.18.19.tar:  6.015:1,  1.330 bits/byte, 83.37% saved, 580761600 in, 96552670 out.

[root@centos ~]# ls -lah
-rw-r--r--. 1 root root 554M Jul 22 10:38 linux-3.18.19.tar
-rw-r--r--. 1 root root  93M Jul 22 10:38 linux-3.18.19.tar.bz2
In this example, a bzipped copy of the Linux kernel has compressed to 83.87% of its original size, taking up 93MB of space rather than 554MB.
6. Adjust compression level
The level of compression applied to a file using bzip2 can be specified as a value between 1 (less compression) and 9 (best compression). Option 1 sets the block size to 100k, option 2 sets it to 200k, all the way up to option 9 which uses 900k. This is because bzip2 compresses files in blocks, the block size affects the compression ratio and amount of memory needed for compression and decompression.
The below example compares the differences between -1 and -9, as shown the -9 option only takes a few extra seconds and increases the compression level by over 3% while testing with the linux kernel.
[root@centos ~]# time bzip2 -v -1 linux-3.18.19.tar
  linux-3.18.19.tar:  5.038:1,  1.588 bits/byte, 80.15% saved, 580761600 in, 115280806 out.

real    1m18.487s
user    1m18.081s
sys     0m0.405s

[root@centos ~]# time bzip2 -v -9 linux-3.18.19.tar
  linux-3.18.19.tar:  6.015:1,  1.330 bits/byte, 83.37% saved, 580761600 in, 96552670 out.

real    1m21.730s
user    1m21.505s
sys     0m0.219s

-1 can also be specified with the flag --fast, while option -9 can also be specified with the flag --best. By default bzip2 uses a compression level of -9, these options are primarily in place for gzip compatibility, for instance --fast doesn’t make things significantly faster as shown above, while --best invokes the default behaviour.
7. Compress a directory
With the help of the tar command, we can create a tar file containing a whole directory and compress the result with bzip2. We can perform the whole lot in one step, as the tar command allows us to specify a compression method to use.
tar cjvf etc.tar.bz2 /etc/
This example creates a compressed etc.tar.bz2 file of the entire /etc/ directory. The tar flags are as follows, ‘c’ creates a new tar archive, ‘j’ specifies that we want to compress with bzip2, ‘v’ provides verbose information, and ‘f’ specifies the file to create. The resulting etc.tar.bz2 file contains all files within /etc/ compressed using bzip2.
8. Integrity test
The -t or --test flag can be used to check the integrity of a compressed file.
On a normal file, the result will be listed as OK, shown below.
[root@centos ~]# bzip2 -tv linux-3.18.19.tar.bz2
  linux-3.18.19.tar.bz2: ok
I have now manually modified this file with a text editor and added a random value, essentially introducing corruption and it is now no longer valid.
[root@centos ~]# bzip2 -tv linux-3.18.19.tar.bz2
  linux-3.18.19.tar.bz2: data integrity (CRC) error in data

You can use the `bzip2recover' program to attempt to recover
data from undamaged sections of corrupted files.
The compressed .bz2 file makes use of cyclic redundancy check (CRC) in order to detect errors. The CRC value can be viewed by running bzip2 command with the -vv flag, as shown below.
[root@centos test]# bzip2 -vv file.txt
  file.txt:
    block 1: crc = 0x3f1075ca, combined CRC = 0x3f1075ca, size = 8
    final combined CRC = 0x3f1075ca
    0.174:1, 46.000 bits/byte, -475.00% saved, 8 in, 46 out.
9. Concatenate multiple files
Multiple files can be concatenated into a single .bz2 file.
bzip2 -c file1.txt > files.bz2
bzip2 -c file2.txt >> files.bz2
The files.bz2 now contains the contents of both file1.txt and file2.txt, if you decompress files.bz2 you will get a file named ‘files’ which contains the content of both .txt files. The output is similar to running ‘cat file1.txt file2.txt’. If instead you want to create a single file that contains multiple files you can use the tar command which supports bzip2 compression, as covered above in example 7.
10. Additional commands included with bzip2
The bzip2 package provides some very useful commands for working with compressed files, such as bzcat, bzgrep and bzless/bzmore.
As you can probably tell by the names of the commands, these are essentially the cat, grep, and less/more commands, however they work directly on compressed data. This means that you can easily view or search the contents of a compressed file without having to decompress it and then view or search it in a second step.
[root@centos test]# bzcat test.txt.bz2
test
example
text
[root@centos test]# bzgrep exa test.txt.bz2
example
This is especially useful when searching through or reviewing log files which have been compressed during log rotation.
dos2unix and unix2dos

The dos2unix package includes the utilities dos2unixand unix2dos to convert plain text files in DOS or Macformat to Unix format, and vice versa.
Description
In DOS/Windows text files, a line break, also known as newline, is a combination of two characters: a Carriage Return (CR) followed by a Line Feed (LF). In Unix text files a line break is a single character: the Line Feed (LF). In Mac text files, prior to Mac OS X, a line break was single Carriage Return (CR) character. Nowadays Mac OS uses Unix style (LF) line breaks.
Binary files are automatically skipped, unless conversion is forced.
Non-regular files, such as directories and FIFOs, are automatically skipped.
Symbolic links and their targets are by default kept untouched. Symbolic links can optionally be replaced, or the output can be written to the symbolic link target. Symbolic links on Windows are not supported. Windows symbolic links are always replaced, keeping the targets unchanged.
Dos2unix was modelled after dos2unix under SunOS/Solaris and has similar conversion modes.
unix2dos and dos2unix syntax
dos2unix [options] [FILE ...] [-n INFILE OUTFILE ...]
unix2dos [options] [FILE ...] [-n INFILE OUTFILE ...]
Options
--
Treat all options that follow as file names. Use this option, for instance, if you want to convert files whose names start with a dash. So, to convert a file named "-foo", you can use this command:
dos2unix -- -foo Or in new file mode:
dos2unix -n -- -foo out.txt
-ascii
Convert only line breaks. This is the default conversion mode.
-iso
Conversion between DOS and ISO-8859-1 character set. See also section CONVERSION MODES.
-1252
Use Windows code page 1252 (Western European).
-437
Use DOS code page 437 (US). This is the default code page used for ISO conversion.
-850
Use DOS code page 850 (Western European)
-860
Use DOS code page 860 (Portuguese).
-863
Use DOS code page 863 (French Canadian).
-865
Use DOS code page 865 (Nordic).
-7
Convert 8 bit characters to 7 bit space.
-c, --convmodeCONVMODE
Set conversion mode. Where CONVMODE is one of: ascii, 7bit, iso, or mac, with asciibeing the default.
-f, --force
Force conversion of binary files.
-h, --help
Display help and exit.
-k, --keepdate
Keep the date stamp of output file same as input file.
-L, --license
Display program's license.
-l, --newline
Add additional newline.
dos2unix: Only DOS line breaks are changed to two Unix line breaks. In Mac mode only Mac line breaks are changed to two Unix line breaks.
unix2dos: Only Unix line breaks are changed to two DOS line breaks. In Mac mode Unix line breaks are changed to two Mac line breaks.
-m, --add-bom
Write an UTF-8 Byte Order Mark in the output file. Never use this option when the output encoding is other than UTF-8. See also section UNICODE.
-n, --newfileINFILE OUTFILE...
New file mode. Convert file INFILE and write output to file OUTFILE. File names must be given in pairs and wildcard names should not be used or you will lose your files.
The person who starts the conversion in new file (paired) mode will be the owner of the converted file. The read/write permissions of the new file will be the permissions of the original file minus the umask of the person who runs the conversion.
-o, --oldfile FILE ...
Old file mode. Convert file FILE and overwrite output to it. The program defaults to run in this mode. Wildcard names may be used.
In old file (in-place) mode the converted file gets the same owner, group, and read/writepermissions as the original file. Also when the file is converted by another user who has write permissions on the file (e.g. user root). The conversion will be aborted when it is not possible to preserve the original values. Change of owner could mean that the original owner is not able to read the file any more. Change of group could be a security risk, the file could be made readable for persons for whom it is not intended. Preservation of owner, group, and read/write permissions is only supported on Unix.
-q, --quiet
Quiet mode. Suppress all warnings and messages. The return value is zero. Except when wrong command-line options are used.
-s, --safe
Skip binary files (default).
-F, --follow-symlink
Follow symbolic links and convert the targets.
-R, --replace-symlink
Replace symbolic links with converted files (original target files remain unchanged).
-S, --skip-symlink
Keep symbolic links and targets unchanged (default).
-V, --version
Display version information and exit.
Mac Mode
In normal mode line breaks are converted from DOS to Unix and vice versa. Mac line breaks are not converted.
In Mac mode line breaks are converted from Mac to Unix and vice versa. DOS line breaks are not changed.
To run in Mac mode use the command-line option "-c mac" or use the commands "mac2unix" or "unix2mac".
Conversion Modes
ascii
In mode "ascii" only line breaks are converted. This is the default conversion mode.
Although the name of this mode is ASCII, which is a 7 bit standard, the actual mode is 8 bit. Use always this mode when converting Unicode UTF-8 files.
7bit
In this mode all 8 bit non-ASCII characters (with values from 128 to 255) are converted to a 7 bit space.
iso
Characters are converted between a DOS character set (code page) and ISO character set ISO-8859-1 (Latin-1) on Unix. DOS characters without ISO-8859-1 equivalent, for which conversion is not possible, are converted to a dot. The same counts for ISO-8859-1 characters without DOS counterpart.
When only option "-iso" is used dos2unix will try to determine the active code page. When this is not possible dos2unix will use default code page CP437, which is mainly used in the USA. To force a specific code page use options "-437" (US), "-850" (Western European), "-860" (Portuguese), "-863" (French Canadian), or "-865" (Nordic). Windows code page CP1252 (Western European) is also supported with option "-1252". For other code pages use dos2unix in combination with iconv. iconvcan convert between a long list of character encodings.
Never use ISO converion on Unicode text files. It will corrupt UTF-8 encoded files.
Some examples:
Convert from DOS default code page to Unix Latin-1:
dos2unix -iso -n in.txt out.txt
Convert from DOS CP850 to Unix Latin-1:
dos2unix -850 -n in.txt out.txt
Convert from Windows CP1252 to Unix Latin-1:
dos2unix -1252 -n in.txt out.txt
Convert from Windows CP1252 to Unix UTF-8 (Unicode):
iconv -f CP1252 -t UTF-8 in.txt | dos2unix > out.txt
Convert from Unix Latin-1 to DOS default code page:
unix2dos -iso -n in.txt out.txt
Convert from Unix Latin-1 to DOS CP850:
unix2dos -850 -n in.txt out.txt
Convert from Unix Latin-1 to Windows CP1252:
unix2dos -1252 -n in.txt out.txt
Convert from Unix UTF-8 (Unicode) to Windows CP1252:
unix2dos < in.txt | iconv -f UTF-8 -t CP1252 > out.txt
See also http://czyborra.com/charsets/codepages.html and http://czyborra.com/charsets/iso8859.html.
NOTE: Conversion modes ascii, 7bit, and iso are similar to those of dos2unix/unix2dos under SunOS/Solaris.
Unicode
Encodings
There exist different Unicode encodings. On Unix and Linux Unicode files are typically encoded in UTF-8 encoding. On Windows Unicode text files can be encoded in UTF-8, UTF-16, or UTF-16 big endian, but are mostly encoded in UTF-16 format.
Conversion
Unicode text files can have DOS, Unix or Mac line breaks, like regular text files.
All versions of dos2unix and unix2dos can convert UTF-8 encoded files, because UTF-8 was designed for backward compatibility with ASCII.
dos2unix and unix2dos with Unicode UTF-16 support can read little and big endian UTF-16 encoded text files. To see if dos2unix was built with UTF-16 support type "dos2unix -V".
The Windows versions of dos2unix and unix2dos convert UTF-16 encoded files always to UTF-8 encoded files. Unix versions of dos2unix/unix2dos convert UTF-16 encoded files to the locale character encoding when it is set to UTF-8. Use the locale command to find out what the locale character encoding is.
Because UTF-8 formatted text files are well supported on both Windows and Unix, dos2unix, and unix2dos have no option to write UTF-16 files. All UTF-16 characters can be encoded in UTF-8. Conversion from UTF-16 to UTF-8 is without loss. UTF-16 files will be skipped on Unix when the locale character encoding is not UTF-8, to prevent accidental loss of text. When an UTF-16 to UTF-8 conversion error occurs, for instance when the UTF-16 input file contains an error, the file will be skipped.
ISO and 7-bit mode conversion do not work on UTF-16 files.
Byte Order Mark
On Windows Unicode text files typically have a Byte Order Mark (BOM), because many Windows programs (including Notepad) add BOMs by default. See also https://en.wikipedia.org/wiki/Byte_order_mark.
On Unix Unicode files typically don't have a BOM. It is assumed that text files are encoded in the locale character encoding.
dos2unix can only detect if a file is in UTF-16 format if the file has a BOM. When an UTF-16 file doesn't have a BOM, dos2unix will see the file as a binary file.
Use dos2unix in combination with iconv to convert an UTF-16 file without BOM.
Dos2unix never writes a BOM in the output file, unless you use option "-m".
Unix2dos writes a BOM in the output file when the input file has a BOM, or when option "-m" is used.
Unicode Examples
Convert from Windows UTF-16 (with BOM) to Unix UTF-8:
dos2unix -n in.txt out.txt
Convert from Windows UTF-16 (without BOM) to Unix UTF-8:
iconv -f UTF-16 -t UTF-8 in.txt | dos2unix > out.txt
Convert from Unix UTF-8 to Windows UTF-8 with BOM:
unix2dos -m -n in.txt out.txt
Convert from Unix UTF-8 to Windows UTF-16:
unix2dos < in.txt | iconv -f UTF-8 -t UTF-16 > out.txt
Recursive Conversion
Use dos2unix in combination with the find and xargs commands to recursively convert text files in a directory tree structure. For instance to convert all .txt files in the directory tree under the current directory type:
find . -name *.txt | xargs dos2unix
Localization
LANG
The primary language is selected with the environment variable LANG. The LANG variable consists out of several parts. The first part is in small letters the language code. The second is optional and is the country code in capital letters, preceded with an underscore. There is also an optional third part: character encoding, preceded with a dot. A few examples for POSIX standard type shells:
export LANG=nl
Dutch
export LANG=nl_NL
Dutch, The Netherlands
export LANG=nl_BE
Dutch, Belgium
export LANG=es_ES
Spanish, Spain
export LANG=es_MX
Spanish, Mexico
export LANG=en_US.iso88591
English, USA, Latin-1 encoding
export LANG=en_GB.UTF-8
English, UK, UTF-8 encoding
For a complete list of language and country codes see the gettext manual: https://www.gnu.org/software/gettext/manual/gettext.html#Language-Codes
On Unix systems you can use to command locale to get locale-specific information.
LANGUAGE
With the LANGUAGE environment variable you can specify a priority list of languages, separated by colons. Dos2unix gives preference to LANGUAGE over LANG. For instance, first Dutch and then German: "LANGUAGE=nl:de". You have to first enable localization, by setting LANG (or LC_ALL) to a value other than "C", before you can use a language priority list through the LANGUAGE variable. See also the gettext manual: https://www.gnu.org/software/gettext/manual/gettext.html#The-LANGUAGE-variable
If you select a language which is not available you will get the standard English messages.
DOS2UNIX_LOCALEDIR
With the environment variable DOS2UNIX_LOCALEDIR the LOCALEDIR set during compilation can be overruled. LOCALEDIR is used to find the language files. The GNU default value is "/usr/local/share/locale". Option --version will display the LOCALEDIR that is used.
Example (POSIX shell):
export DOS2UNIX_LOCALEDIR=$HOME/share/locale
Return Values
On success, zero is returned. When a system error occurs the last system error will be returned. For other errors 1 is returned.
The return value is always zero in quiet mode, except when wrong command-line options are used.
unix2dos and dos2unix examples
dos2unix
Get input from stdin and write output to stdout.
dos2unix a.txt b.txt
dos2unix -o a.txt b.txt
Both of the above commands will do the same thing: convert, and replace, both a.txt and b.txt in one command.
dos2unix -k a.txt
Converts and replaces a.txt while keeping original date stamp.

Tail

The tail command displays the last ten lines of the file.
Syntax
The syntax for the tail command is:
tail [options] [file]
Options
Option
Description
-f
Follow the file as it grows.
-r
Displays the lines in the reverse order.
-n[k]
Displays the file at the nth item from the end of the file.
+n[k]
Displays the file at the nth item from the beginning of the file.
Example
tail -r tech

passwd

The passwd command is used to change the password of a user account. A normal user can run passwd to change their own password, and a system administrator (the superuser) can use passwd to change another user's password, or define how that account's password can be used or changed.
passwd syntax
passwd [OPTION] [USER]
Quick Examples
Change Your Password
passwd
Running passwd with no options will change the password of the account running the command. You will first be prompted to enter the account's current password:
(current) UNIX password:
If it is correct, you will then be asked to enter a new password:
Enter new UNIX password:
...and to enter the same password again, to verify it:
Retype new UNIX password:
If the passwords match, the password will be changed.
Change Another User's Password
sudo passwd jeff
If you have superuser privileges, you can change another user's password. Here, we prefix the command with sudo to run it as the superuser. This command will change the password for user jeff. You will not be prompted for jeff's current password.
Change Your Password Without Knowing Your Current Password
If you need to change your password because you forgot it, you will need to log in to the root account. To do this, you will need to know the password for user root.
Let's say your user name is sally, and you can't remember your password. However, you have administrator access to the system: you can log in as root, using the password for that account. Log in as root, and then from the command line, run:
passwd sally
But what if you forgot the password for root as well? In this case, you will need to log in to the machine in single-user mode, also known as Runlevel 1. This cannot be done over the network, so you will need physical access to the machine to boot into this runlevel.
Reboot the machine. When it is booting up, you should be presented with a bootloader menu. On many systems, such as Debian or Ubuntu, the boot menu will include an option for "Recovery Mode" or "Single User Mode" (as in the image below). Select this boot option.

This option will boot you into a text-only mode, and log you in as root.
If you need to mount /, do so:
mount -rw -o remount /
Now change sally's password:
passwd sally
Or root's:
passwd
When you're done, reboot your system:
shutdown -r now
Start the system normally, and you should be able to log in as sally with the new password.
Now that we've gone over the most common scenarios for using passwd, let's look at the command in more detail. The following sections will describe how the command works, how it can be used, and what options can be specified to make use of its different functions.
Description
The passwd command changes passwords for user accounts. A normal user can only change the password for their own account, but the superuser can change the password for any account. passwdcan also change or reset the account's validity period — how much time can pass before the password expires and must be changed.
Before a normal user can change their own password, they must first enter their current password for verification. (The superuser can bypass this step when changing another user's password.)
After the current password has been verified, passwd checks to see if the user is allowed to change their password at this time. If not, passwd refuses to continue, and exits.
Otherwise, the user is then prompted twice for a replacement password. Both entries must match for passwd to continue.
Next, the password is tested for complexity. As a general guideline, passwords should consist of at least 6 characters, including one or more of each of the following:
lower case letters
digits 0 through 9
punctuation marks
Options
The following options will change the way passwd operates:
-a, --all
When used with -S (see below), this option will show the password status for all users. This option will not work if used without -S.
-d, --delete
Delete a user's password (make it empty). This option is a quick way to disable logins for an account, without disabling the account itself.
-e, --expire
Immediately expire an account's password. This forces a user to change their password the next time they log in.
-h, --help
Display information about how to use the passwd command.
-i, --inactive INACTIVE
This option is used to disable an account after the password has been expired for a number of days. After a user account has had an expired password for integer INACTIVE days, the user may no longer sign on to the account.
-k, --keep-tokens
Keep password tokens. Indicates that this user's password should only be changed if it has expired.
-l, --lock
Lock the password of the named account. This option disables a password by changing it to a value which matches no possible encrypted value. It does this by adding a character at the beginning of the encrypted password.

Note that this does not disable the account. The user may still be able to log in using another authentication method (an SSH key, for example). To disable the account, the superuser can use the usermod command with the option --expiredate 1. This option will set the account's expiration date to a date in the past — namely Jan 2, 1970.

Users with a locked password are not allowed to change their password.
-n, --mindays MIN_DAYS
Set the minimum number of days between password changes to MIN_DAYS. A value of zero for this field indicates that the user may change his/her password at any time.
-q, --quiet
Quiet mode; passwd will operate without displaying any output.
-R, --root CHROOT_DIR
For advanced users: this option will apply changes in the chroot directory CHROOT_DIR and use the configuration files from the CHROOT_DIR directory.
-S, --status
Display account status information. The status information consists of 7 fields:
1. The user's login name
2. password usability: L if the account has a locked password, NP if the account has no password, or P if the account has a usable password
3. date of the last password change
4. minimum password age
5. maximum password age
6. password warning period
7. password inactivity period

In fields 4 through 7, password ages are expressed in days.

Specifying -a in addition to -S will display password status for all users.
-u, --unlock
Unlock the password of the named account. This option re-enables a password by changing the password back to its value before the -l option was used to lock it.
-w, --warndays WARN_DAYS
Set the number of days of warning before a password change is required. WARN_DAYS is the number of days prior to the password expiring that a user will be warned that their password is about to expire.
-x, --maxdays MAX_DAYS
Set the maximum number of days a password remains valid. After MAX_DAYS, the password must be changed.
Notes
Password complexity will vary depending on the system. Consult your operating system documentation for default complexity rules and how to change them.
On systems that use NIS (Network Information Services), users may not be able to change their password if they are not logged into the NIS server.
System Files Used By Passwd
/etc/passwd
User account information.
/etc/shadow
Secure user account information.
/etc/pam.d/passwd
PAM configuration for passwd.
passwd examples
passwd
Change your password.
sudo passwd username
Change the password for the user named username.
sudo passwd -S ted
Check the status of the password for the user named ted. Output will resemble the following:
ted P 05/13/2014 2 365 7 28
Here, we see the user's name (ted), followed by a P, indicating that his password is currently valid and usable. The password will expire on May 5, 2014. Ted cannot change his password more often than every 2 days, and must change the password every 365 days. He will be warned 7 days before a required password change, and if he allows his password to expire, his account will be disabled 28days later.
sudo passwd -S -a
Similar to the above command, but checks the password status for all user accounts, system-wide.
sudo passwd -l jane
Lock the password for user jane. She will be unable to log in until a system administrator unlocks it.
sudo passwd -u jane
Unlock jane's password. It will automatically be reset to whatever it was before it was locked, and she will be able to log in again.
sudo passwd -e alan
Expire alan's password. The next time he logs in, he will be required to set a new password.
Cat

cat stands for "catenate." It reads data from files, and outputs their contents. It is the simplest way to display the contents of a file at the command line.
Overview
cat is one of the most commonly-used commands in Linux. It can be used to:
Display text files
Copy text files into a new document
Append the contents of a text file to the end of another text file, combining them
Displaying Text Files
The simplest way to use cat is to give it the name of a text file. It will display the contents of the text file on the screen. For instance:
cat mytext.txt
...will read the contents of mytext.txt and send them to standard output (your terminal screen). If mytext.txt is very long, they will zoom past and you will only see the last screen's worth of your document.
If you want to view the document page-by-page or scroll back and forth through the document, you can use a pager or viewer such as pg, more, or less.
If you specify more than one file name, cat will display those files one after the other, catenating their contents to standard output. So this command:
cat mytext.txt mytext2.txt
Will print the contents of those two text files as if they were a single file.
Copy A Text File
Normally you would copy a file with the cp command. You can use cat to make copies of text files in much the same way.
cat sends its output to stdout (standard output), which is usually the terminal screen. However, you can redirect this output to a file using the shell redirection symbol ">".
For instance, this command:
cat mytext.txt > newfile.txt
...will read the contents of mytext.txt and send them to standard output; instead of displaying the text, however, the shell will redirect the output to the file newfile.txt. If newfile.txt does not exist, it will be created. If newfile.txt already exists, it will be overwritten and its previous contents will be lost, so be careful.
Similarly, you can catenate several files into your destination file. For instance:
cat mytext.txt mytext2.txt > newfile.txt
...will read the contents of mytext.txt and mytext2.txt and write the combined text to the file newfile.txt. Again, if newfile.txt does not already exist, it will be created; if it already exists, it will be overwritten.
Append A Text File's Contents To Another Text File
Instead of overwriting another file, you can also append a source text file to another using the redirection operator ">>".
For instance:
cat mytext.txt >> another-text-file.txt
...will read the contents of mytext.txt, and write them at the end of another-text-file.txt. If another-text-file.txt does not already exist, it will be created and the contents of mytext.txt will be written to the new file.
The cat command also works for multiple text files as well:
cat mytext.txt mytext2.txt >> another-text-file.txt
...will write the combined contents of mytext.txt and mytext2.txt to the end of another-text-file.txt.
Incorporating Standard Input Into cat Output
cat reads from standard input if you specify a hyphen ("-") as a file name. For example, if you have a file, list.txt, which contains the following text:
apples
oranges
butter
bread
...you could use the echo command to output text, pipe that output to cat, and instruct cat to catenate it with the file's contents, like this:
echo "My Shopping List" | cat - list.txt
...which would output the following text:
My Shopping List
apples
oranges
butter
bread
In short, cat is a simple but very useful tool for working with the data in text files, system logs, configuration files, and any other human-readable data stored in a file.
cat syntax
cat [OPTION]... [FILE]...
Options
These options are available on GNU cat, which is standard on most Linux distributions. If you are using a different Unix-like operating system (BSD, for example), some of these options may not be available; check your specific documentation for details.
-A, --show-all
Equivalent to -vET.
-b, --number-nonblank
Number non-empty output lines. This option overrides -n.
-e
Equivalent to -vE.
-E, --show-ends
Display "$" at end of each line.
-n, --number
Number all output lines.
-s, --squeeze-blank
Suppress repeated empty output lines.
-t
Equivalent to -vT.
-T, --show-tabs
Display TAB characters as ^I.
-v, --show-nonprinting
Use ^ and M- notation, except for LFD and TAB.
--help
Display a help message, and exit.
--version
Output version information, and exit.
cat examples
cat file.txt
Read the contents of file.txt and display them on the screen.
cat file1.txt file2.txt
Reads the contents of file1.txt and file2.txt, and displays them in order on the terminal screen.
cat file.txt > newfile.txt
Read the contents of file.txt and write them to newfile.txt, overwriting anything newfile.txt previously contained. If newfile.txt does not exist, it will be created.
cat file.txt >> another-file.txt
Read the contents of file.txt and append them to the end of another-file.txt. If another-file.txt does not exist, it will be created.
cat -s file.txt
Display the contents of file.txt, omitting any repeated blank lines.


Env

env is a shell command for Linux, Unix, and Unix-like operating systems. It can be used to print a list of the current environment variables, or to run another program in a custom environment without modifying the current one.
Description
If env is run without any options, it prints the variables of the current environment. Otherwise, env sets each NAME to VALUE and executes COMMAND.
env syntax
env [OPTION]... [-] [NAME=VALUE]... [COMMAND [ARG]...]
Options
-i, --ignore-environment
Start with an empty environment.
-0, --null
End each output line with a 0 (null) byte rather than a newline.
-u, --unset=NAME
Remove variable NAME from the environment.
--help
Display a help message and exit.
--version
Display version information and exit.
-
Same as -i.
env examples
env
Executing env with no options displays the current environment variables and their values. Output will look similar to the following:
HOME=/computerhope/public_html
PATH=/usr/local/bin:
LOGNAME=admin
HZ=100
TERM=vt100
TZ=MST7MDT
SHELL=/bin/csh
MAIL=/var/mail/computerhope
_INIT_UTS_PLATFORM=SUNW,SPARCstation-10
_INIT_UTS_RELEASE=5.7
_INIT_UTS_SYSNAME=SunOS
_INIT_UTS_VERSION=Generic_106541-08
EDITOR=pico -t
OPENWINHOME=/usr/openwin
MANPATH=/usr/man:/usr/local/man:/usr/openwin/man
LD_LIBRARY_PATH=/usr/local/lib:/usr/openwin/lib
PAGER=more
Below is brief description of some commonly-used environment variables:
EDITOR
The default file editor to be used.
HOME
The current user's home directory.
SHELL
The location of the current user's shell program.
TERM
The current terminal emulation.
PATH
Pathnames to be searched when executing commands.
MAIL
Location of where mail is to be stored.
MANPATH
Location of your Manuals. See man command.
LOGNAME
The name of the current user.
TZ
The time zone used by the system clock.


fuser
fuser identifies processes using files or sockets.
Description
fuser displays the PIDs of processes using the specified files or file systems.
In the default display mode, each file name is followed by a letter denoting the type of access:
c
current directory.
e
executable being run.
f
open file. f is omitted in default display mode.
F
open file for writing. F is omitted in default display mode.
r
root directory.
m
mmap'ed file or shared library.
fuser returns a non-zero return code if none of the specified files is accessed or in case of a fatal error. If at least one access has been found, fuser returns zero.
To look up processes using TCP and UDP sockets, the corresponding name space has to be selected with the -n option. By default fuser will look in both IPv6 and IPv4 sockets. To change the default behavior, use the -4 and -6 options. The socket(s) can be specified by the local and remote port, and the remote address. All fields are optional, but commas in front of missing fields must be present:
[lcl_port][,[rmt_host][,[rmt_port]]]
Either symbolic or numeric values can be used for IP addresses and port numbers.
fuser outputs only the PIDs to stdout, everything else is sent to stderr.
fuser syntax
fuser [-fuv] [-a|-s] [-4|-6] [-c|-m|-n space] [ -k [-i] [-M] [-w]
      [-SIGNAL] ] name ...
fuser -l
fuser -V
Options
-a, --all
Show all files specified on the command line. By default, only files that are accessed by at least one process are shown.
-c
Same as -m option, used for POSIX compatibility.
-f
Silently ignored, used for POSIX compatibility.
-k, --kill
Kill processes accessing the file. Unless changed with -SIGNAL, SIGKILL is sent. An fuserprocess never kills itself, but may kill other fuser processes. The effective user ID of the process executing fuser is set to its real user ID before attempting to kill.
-i, --interactive
Ask the user for confirmation before killing a process. This option is silently ignored if -k is not also present.
-l, --list-signals
List all known signal names.
-m NAME, --mount NAME
NAME specifies a file on a mounted file system or a block device that is mounted. All processes accessing files on that file system are listed. If a directory file is specified, it is automatically changed to NAME/. to use any file system that might be mounted on that directory.
-M, --ismountpoint
Request will be fulfilled only if NAME specifies a mountpoint. This is an invaluable seatbelt which prevents you from killing the machine if NAME happens to not be a filesystem.
-w
Kill only processes which have write access. This option is silently ignored if -k is not also present.
-n SPACE, --namespaceSPACE
Select a different name space. The name spaces file (file names, the default), udp (local UDP ports), and tcp (local TCP ports) are supported. For ports, either the port number or the symbolic name can be specified. If there is no ambiguity, the shortcut notation name/space (e.g. 80/tcp) can be used.
-s, --silent
Silent operation. -u and -v are ignored in this mode. -a must not be used with -s.
-SIGNAL
Use the specified signal instead of SIGKILL when killing processes. Signals can be specified either by name (e.g. -HUP) or by number (e.g. -1). This option is silently ignored if the -koption is not also present.
-u, --user
Append the user name of the process owner to each PID.
-v, --verbose
Verbose mode. Processes are shown in a ps-like style. The fields PID, USER, and COMMAND are similar to ps. ACCESS shows how the process accesses the file. Verbose mode will also show when a particular file is being access as a mount point, knfs export or swap file. In this case kernel is shown instead of the PID.
-V, --version
Display version information.
-4, --ipv4
Search only for IPv4 sockets. This option must not be used with the -6 option and only has an effect with the tcp and udp namespaces.
-6, --ipv6
Search only for IPv6 sockets. This option must not be used with the -4 option and only has an effect with the tcp and udp namespaces.
-
Reset all options and set the signal back to SIGKILL.
fuser examples
fuser .
Display every process ID that is using the current directory ("./").
fuser -v .
Display verbose information about every process that is using the current directory. This information includes the name of the user who initiated the process and an indicator of the process name.
fuser -v /
Display verbose information about every process that is using the root directory.


tty
A tty command in Linux and other Unix-like operating systems is a shell command that can be entered interactively or as part of a script to determine whether the output for the script is a terminal (that is, to an interactive user) or to some other destination such as another program or a printer

Exec

Exec may refer to any of the following:
1. When referring to a command line such as Linux or Unix, exec is a BOURNE and POSIX shell command that replaces the current shell process with the command specified after exec. This command does not create a new PID. For example, if you were to run exec <command>, the shell would be replaced by that command. When that command is exited, the shell will exit.
Tip: If you're trying to execute a script or program use type ./ in front of the script or program, don't use exec.



Backtick or reverse quote or Grave accent

This is a backtick. Backtick is not a quotation sign, it has a very special meaning. Everything you type between backticks is evaluated (executed) by the shell before the main command (like chown in your examples), and the output of that execution is used by that command, just as if you'd type that output at that place in the command line.
So, what
sudo chown `id -u` /somedir

WHAT ARE VARIABLES IN SHELL SCRIPTING?
A variable is a value holder which we can change when it is required. We can use these variables in our shell scripts so that we no need to hard code the values with the shell script.
1. System variables
2. User defined variables
3. Special variables
Positional parameters
Special variables
We already discussed System variables, Some special variables, and command exit status in our other posts. Before learning positional we should know how we pass variables to a shell script.
HOW TO PASS VARIABLES IN SHELL SCRIPTING?
We can pass variables into shell scripts in different ways to avoid hard coding of values. We have different ways where we can pass variables to a shell script. Positional parameters are one kind of passing variables into shell scripting. Below are the way we can pass variables into shell scripting depending on what time you want to send them to a script.
Within shell script(Variables defined with the script)
Before start of shell script(Positional parameters)
At the time of executing a shell script(using read command)
WHAT ARE POSITIONAL PARAMETERS?
Positional parameters are also called as command line arguments which we pass to the script on the fly. To understand them, take ls command as an example. The ls command has many options like -l for long listing. The option -l is a positional parameter for ls command. Suppose when we use cp command show below.
cp test/ bash/
Where test/ is my first positional parameter and bash/ is my second positional parameter. In this way, we can send variables to a shell script on the fly.
For people who want to see all these variables in one place, below list is for you.
$0: contains the name of script as it is invoked
$1, $2, …, $n: indicates the position of the argument also called as positional parameters.
$*: contains all the arguments regrouped as one argument
$@: contains all the arguments, one argument per parameter
$#: contains the number of parameters passed to the script
$? : contains the return code of the previous command (it equaled 0 when the last command was executed successfully)
$$: contains the PID of shell executing the script
$! : contains the PID of last background process
$_ : Last argument of an executed command
Related concept:   25+ Awesome Linux/Unix command chaining examples
Examples:
Let’s create the script test.sh like below:

#/bin/bash
function myFunction () {
echo -e "--------------------------------------------"
echo -e "Name of the script: $0"
echo -e "--------------------------------------------"
echo -e "the arguments regrouped as one argument: $*"
echo -e "--------------------------------------------"
echo -e "the arguments, one argument per parameter: $@"
echo -e "--------------------------------------------"
echo -e "the number of parameters: $#"
echo -e "--------------------------------------------"
echo -e "the first arg: $1"
echo -e "the second arg: $2"
echo -e "the third arg: $3"
echo -e "--------------------------------------------"
echo -e "the return code: $?"
echo -e "--------------------------------------------"
echo -e "the PID of shell executing the script: $$"
echo -e "--------------------------------------------"
echo -e "the PID of last background process: $!"
echo -e "--------------------------------------------"
}
# Launch a background process
# & is used to launch a process in background
sleep 5 &
# Call the function
myFunction $1 $2 $3
Let’s run the script
user@server:~ $ bash test.sh arg1 arg2 arg3
--------------------------------------------
Name of the script: test.sh
--------------------------------------------
the arguments regrouped as one argument: arg1 arg2 arg3
--------------------------------------------
the arguments, one argument per parameter: arg1 arg2 arg3
--------------------------------------------
the number of parameters: 3
--------------------------------------------
the first arg: arg1
the second arg: arg2
the third arg: arg3
--------------------------------------------
the return code: 0
--------------------------------------------
the PID of shell executing the script: 32117
--------------------------------------------
the PID of last background process: 32118
--------------------------------------------
HOW MANY POSITIONAL PARAMETERS ARE THERE?
We can say they are infinity, But there is a slight change when calling positional parameters more than nine.
POSITIONAL PARAMETERS IN LINUX/UNIX
We can divide positional parameters into batches. This segregation is done on basics of how we call them in the shell scripts.
BATCH 1: $1, $2, $3, $4, $5, $6, $7, $8, $9
We already saw how to use these from above example. They are very straight forward where you can pass values at the time of execution and call those values using $1 to $9.
Batch 2: From $10 to $n We call them in a different way.
We can not pass $10 to above values as positional parameters by default, we have to pass in a different way. See below example.
My script abc.sh content
#!/bin/bash
echo "My first positional parameter is $1"
echo "My 10th positional parameter is $10"
Executing it:
bash abc.sh 24 surendra abc xyz red 12 as face 89 kumar
Output:
My first positional parameter is 24 My 10th positional parameter is 240
If you observe my $10 is return as 240 instead of kumar. This is because bash does not know how to read $10. For this, we have to use braces across variable as ${10}. The same example with this change.
#!/bin/bash echo "My first positional parameter is $1" echo "My 10th positional parameter is ${10}"
Executing it:
bash abc.sh 24 surendra abc xyz red 12 as face 89 kumar
Output:
My first positional parameter is 24 My 10th positional parameter is kumar
DIFFERENCE BETWEEN $@ AND $*
When they are quoted they behave same. The $@ will consider spaces in variables
Positional parameters in for loops
Couple of for loop examples are
Example 1:for i in $@
do
echo $i
Done
Example 2:
for i
 Do
 Echo $i
 Done
I hope that this blog helped you. Please visit our website for other interesting blogs and feel free to leave your feedbacks and thoughts. Till next time!

##############################################################################
How do I set environment variables on UNIX systems?

UNIX and all UNIX-like operating systems such as OpenBSD, Linux, Redhat, CentOS, Debian allows you to set environment variables. When you log in on UNIX, your current shell (login shell) sets a unique working environment for you which is maintained until you log out. Following are most command examples of environment variables used under UNIX operating systems:
PATH – Display lists directories the shell searches, for the commands.
HOME – User’s home directory to store files.
TERM – Set terminal emulator being used by UNIX.
PS1 – Display shell prompt in the Bourne shell and variants.
MAIL – Path to user’s mailbox.
TEMP – Path to where processes can store temporary files.
JAVA_HOME – Sun (now Oracle) JDK path.
ORACLE_HOME – Oracle database installation path.
TZ – Timezone settings
PWD – Path to the current directory.
HISTFILE – The name of the file in which command history is saved
HISTFILESIZE -The maximum number of lines contained in the history file
HOSTNAME -The system’s host name
LD_LIBRARY_PATH -It is a colon-separated set of directories where libraries should be searched for.
USER -Current logged in user’s name.
DISPLAY -Network name of the X11 display to connect to, if available.
SHELL -The current shell.
TERMCAP – Database entry of the terminal escape codes to perform various terminal functions.
OSTYPE – Type of operating system.
MACHTYPE – The CPU architecture that the system is running on.
EDITOR – The user’s preferred text editor.
PAGER – The user’s preferred text pager.
MANPATH – Colon separated list of directories to search for manual pages.
Display Environment Variable
Open the terminal and type the following commands to display all environment variables and their values under UNIX-like operating systems:
$ set
OR
$ printenv
OR
$ env
Sample outputs:

To display search path, enter:
echo $PATH
To display prompt settings, enter:
echo $PS1
A few more examples:
echo $USER
echo $PWD
echo $MAIL
echo $JAVA_PATH
echo $DB2INSTANCE
Change or Set Environment Variable
You can use the following command to change the environment variable for the current session as per your shell.
For Korn shell (KSH)
The syntax is as follows:
var=value
export var
To set JAVA_PATH, enter:
JAVA_PATH=/opt/jdk/bin
export JAVA_PATH
For Bourne shell (sh and bash)
The syntax is as follows:
export var=value
To set PATH, enter:
export PATH=$PATH:/opt/bin:/usr/local/bin:$HOME/bin
For C shell (csh or tcsh)
The syntax is as follows:
setenv var value
Set EDITOR to vim, enter:
setenv EDITOR vim

################################################################################

for loop syntax
Numeric ranges for syntax is as follows:
for VARIABLE in 1 2 3 4 5 .. N
do
        command1
        command2
        commandN
done
OR
for VARIABLE in file1 file2 file3
do
        command1 on $VARIABLE
        command2
        commandN
done
OR
for OUTPUT in $(Linux-Or-Unix-Command-Here)
do
        command1 on $OUTPUT
        command2 on $OUTPUT
        commandN
done
Examples

This type of for loop is characterized by counting. The range is specified by a beginning (#1) and ending number (#5). The for loop executes a sequence of commands for each member in a list of items. A representative example in BASH is as follows to display welcome message 5 times with for loop:
#!/bin/bash
for i in 1 2 3 4 5
do
   echo "Welcome $i times"
done
Sometimes you may need to set a step value (allowing one to count by two’s or to count backwards for instance). Latest bash version 3.0+ has inbuilt support for setting up ranges:
#!/bin/bash
for i in {1..5}
do
   echo "Welcome $i times"
done
Bash v4.0+ has inbuilt support for setting up a step value using {START..END..INCREMENT} syntax:
#!/bin/bash
echo "Bash version ${BASH_VERSION}..."
for i in {0..10..2}
  do 
     echo "Welcome $i times"
 done
Sample outputs:
Bash version 4.0.33(0)-release...
Welcome 0 times
Welcome 2 times
Welcome 4 times
Welcome 6 times
Welcome 8 times
Welcome 10 times
The seq command (outdated)
WARNING! The seq command print a sequence of numbers and it is here due to historical reasons. The following examples is only recommend for older bash version. All users (bash v3.x+) are recommended to use the above syntax.
The seq command can be used as follows. A representative example in seq is as follows:
#!/bin/bash
for i in $(seq 1 2 20)
do
   echo "Welcome $i times"
done
There is no good reason to use an external command such as seq to count and increment numbers in the for loop, hence it is recommend that you avoid using seq. The builtin command are fast.
Three-expression bash for loops syntax
This type of for loop share a common heritage with the C programming language. It is characterized by a three-parameter loop control expression; consisting of an initializer (EXP1), a loop-test or condition (EXP2), and a counting expression (EXP3).
for (( EXP1; EXP2; EXP3 ))
do
        command1
        command2
        command3
done
A representative three-expression example in bash as follows:
#!/bin/bash
for (( c=1; c<=5; c++ ))
do  
   echo "Welcome $c times"
done
Sample output:
Welcome 1 times
Welcome 2 times
Welcome 3 times
Welcome 4 times
Welcome 5 times
How do I use for as infinite loops?
Infinite for loop can be created with empty expressions, such as:
#!/bin/bash
for (( ; ; ))
do
   echo "infinite loops [ hit CTRL+C to stop]"
done
Conditional exit with break
You can do early exit with break statement inside the for loop. You can exit from within a FOR, WHILE or UNTIL loop using break. General break statement inside the for loop:
for I in 1 2 3 4 5
do
  statements1      #Executed for all values of ''I'', up to a disaster-condition if any.
  statements2
  if (disaster-condition)
  then
        break              #Abandon the loop.
  fi
  statements3          #While good and, no disaster-condition.
done
Following shell script will go though all files stored in /etc directory. The for loop will be abandon when /etc/resolv.conf file found.
#!/bin/bash
for file in /etc/*
do
        if [ "${file}" == "/etc/resolv.conf" ]
        then
                countNameservers=$(grep -c nameserver /etc/resolv.conf)
                echo "Total  ${countNameservers} nameservers defined in ${file}"
                break
        fi
done
Early continuation with continue statement
To resume the next iteration of the enclosing FOR, WHILE or UNTIL loop use continue statement.
for I in 1 2 3 4 5
do
  statements1      #Executed for all values of ''I'', up to a disaster-condition if any.
  statements2
  if (condition)
  then
        continue   #Go to next iteration of I in the loop and skip statements3
  fi
  statements3
done
This script make backup of all file names specified on command line. If .bak file exists, it will skip the cp command.
#!/bin/bash
FILES="$@"
for f in $FILES
do
        # if .bak backup file exists, read next file
        if [ -f ${f}.bak ]
        then
                echo "Skiping $f file..."
                continue  # read next file and skip the cp command
        fi
        # we are here means no backup file exists, just use cp command to copy file
        /bin/cp $f $f.bak
done



Substitution


What is Substitution?
The shell performs substitution when it encounters an expression that contains one or more special characters.
Example
Here, the printing value of the variable is substituted by its value. Same time, "\n" is substituted by a new line −
#!/bin/sh

a=10
echo -e "Value of a is $a \n"
You will receive the following result. Here the -e option enables the interpretation of backslash escapes.
Value of a is 10
Following is the result without -e option −
Value of a is 10\n
Here are following escape sequences which can be used in echo command −
S.No.
Escape & Description
1
\\
backslash
2
\a
alert (BEL)
3
\b
backspace
4
\c
suppress trailing newline
5
\f
form feed
6
\n
new line
7
\r
carriage return
8
\t
horizontal tab
9
\v
vertical tab
You can use the -E option to disable the interpretation of the backslash escapes (default).
You can use the -n option to disable the insertion of a new line.
Command Substitution
Command substitution is the mechanism by which the shell performs a given set of commands and then substitutes their output in the place of the commands.
Syntax
The command substitution is performed when a command is given as −
`command`
When performing the command substitution make sure that you use the backquote, not the single quote character.
Example
Command substitution is generally used to assign the output of a command to a variable. Each of the following examples demonstrates the command substitution −
#!/bin/sh

DATE=`date`
echo "Date is $DATE"

USERS=`who | wc -l`
echo "Logged in user are $USERS"

UP=`date ; uptime`
echo "Uptime is $UP"
Upon execution, you will receive the following result −
Date is Thu Jul  2 03:59:57 MST 2009
Logged in user are 1
Uptime is Thu Jul  2 03:59:57 MST 2009
03:59:57 up 20 days, 14:03,  1 user,  load avg: 0.13, 0.07, 0.15
Variable Substitution
Variable substitution enables the shell programmer to manipulate the value of a variable based on its state.
Here is the following table for all the possible substitutions −
S.No.
Form & Description
1
${var}
Substitute the value of var.
2
${var:-word}
If var is null or unset, word is substituted for var. The value of var does not change.
3
${var:=word}
If var is null or unset, var is set to the value of word.
4
${var:?message}
If var is null or unset, message is printed to standard error. This checks that variables are set correctly.
5
${var:+word}
If var is set, word is substituted for var. The value of var does not change.
Example
Following is the example to show various states of the above substitution −
#!/bin/sh

echo ${var:-"Variable is not set"}
echo "1 - Value of var is ${var}"

echo ${var:="Variable is not set"}
echo "2 - Value of var is ${var}"

unset var
echo ${var:+"This is default value"}
echo "3 - Value of var is $var"

var="Prefix"
echo ${var:+"This is default value"}
echo "4 - Value of var is $var"

echo ${var:?"Print this message"}
echo "5 - Value of var is ${var}"
Upon execution, you will receive the following result −
Variable is not set
1 - Value of var is
Variable is not set
2 - Value of var is Variable is not set

3 - Value of var is
This is default value
4 - Value of var is Prefix
Prefix
5 - Value of var is Prefix

Quoting Mechanisms

In this chapter, we will discuss in detail about the Shell quoting mechanisms. We will start by discussing the metacharacters.
The Metacharacters
Unix Shell provides various metacharacters which have special meaning while using them in any Shell Script and causes termination of a word unless quoted.
For example, ? matches with a single character while listing files in a directory and an *matches more than one character. Here is a list of most of the shell special characters (also called metacharacters) −
* ? [ ] ' " \ $ ; & ( ) | ^ < > new-line space tab
A character may be quoted (i.e., made to stand for itself) by preceding it with a \.
Example
Following example shows how to print a * or a ? −
#!/bin/sh

echo Hello; Word
Upon execution, you will receive the following result −
Hello
./test.sh: line 2: Word: command not found

shell returned 127
Let us now try using a quoted character −
#!/bin/sh

echo Hello\; Word
Upon execution, you will receive the following result −
Hello; Word
The $ sign is one of the metacharacters, so it must be quoted to avoid special handling by the shell −
#!/bin/sh

echo "I have \$1200"
Upon execution, you will receive the following result −
I have $1200
The following table lists the four forms of quoting −
S.No.
Quoting & Description
1
Single quote
All special characters between these quotes lose their special meaning.
2
Double quote
Most special characters between these quotes lose their special meaning with these exceptions −
$
`
\$
\'
\"
\\
3
Backslash
Any character immediately following the backslash loses its special meaning.
4
Back quote
Anything in between back quotes would be treated as a command and would be executed.
The Single Quotes
Consider an echo command that contains many special shell characters −
echo <-$1500.**>; (update?) [y|n]
Putting a backslash in front of each special character is tedious and makes the line difficult to read −
echo \<-\$1500.\*\*\>\; \(update\?\) \[y\|n\]
There is an easy way to quote a large group of characters. Put a single quote (') at the beginning and at the end of the string −
echo '<-$1500.**>; (update?) [y|n]'
Characters within single quotes are quoted just as if a backslash is in front of each character. With this, the echo command displays in a proper way.
If a single quote appears within a string to be output, you should not put the whole string within single quotes instead you should precede that using a backslash (\) as follows −
echo 'It\'s Shell Programming'
The Double Quotes
Try to execute the following shell script. This shell script makes use of single quote −
VAR=ZARA
echo '$VAR owes <-$1500.**>; [ as of (`date +%m/%d`) ]'
Upon execution, you will receive the following result −
$VAR owes <-$1500.**>; [ as of (`date +%m/%d`) ]
This is not what had to be displayed. It is obvious that single quotes prevent variable substitution. If you want to substitute variable values and to make inverted commas work as expected, then you would need to put your commands in double quotes as follows −
VAR=ZARA
echo "$VAR owes <-\$1500.**>; [ as of (`date +%m/%d`) ]"
Upon execution, you will receive the following result −
ZARA owes <-$1500.**>; [ as of (07/02) ]
Double quotes take away the special meaning of all characters except the following −
$ for parameter substitution
Backquotes for command substitution
\$ to enable literal dollar signs
\` to enable literal backquotes
\" to enable embedded double quotes
\\ to enable embedded backslashes
All other \ characters are literal (not special)
Characters within single quotes are quoted just as if a backslash is in front of each character. This helps the echo command display properly.
If a single quote appears within a string to be output, you should not put the whole string within single quotes instead you should precede that using a backslash (\) as follows −
echo 'It\'s Shell Programming'
The Backquotes
Putting any Shell command in between backquotes executes the command.
Syntax
Here is the simple syntax to put any Shell command in between backquotes −
Syntax
var = `command`
Example
The date command is executed in the following example and the produced result is stored in DATA variable.
DATE=`date`

echo "Current Date: $DATE"
Upon execution, you will receive the following result −
Current Date: Thu Jul  2 05:28:45 MST 2009

Input/Output Redirections

In this chapter, we will discuss in detail about the Shell input/output redirections. Most Unix system commands take input from your terminal and send the resulting output back to your terminal. A command normally reads its input from the standard input, which happens to be your terminal by default. Similarly, a command normally writes its output to standard output, which is again your terminal by default.
Output Redirection
The output from a command normally intended for standard output can be easily diverted to a file instead. This capability is known as output redirection.
If the notation > file is appended to any command that normally writes its output to standard output, the output of that command will be written to file instead of your terminal.
Check the following who command which redirects the complete output of the command in the users file.
$ who > users
Notice that no output appears at the terminal. This is because the output has been redirected from the default standard output device (the terminal) into the specified file. You can check the users file for the complete content −
$ cat users
oko         tty01   Sep 12 07:30
ai          tty15   Sep 12 13:32
ruth        tty21   Sep 12 10:10
pat         tty24   Sep 12 13:07
steve       tty25   Sep 12 13:03
$
If a command has its output redirected to a file and the file already contains some data, that data will be lost. Consider the following example −
$ echo line 1 > users
$ cat users
line 1
$
You can use >> operator to append the output in an existing file as follows −
$ echo line 2 >> users
$ cat users
line 1
line 2
$
Input Redirection
Just as the output of a command can be redirected to a file, so can the input of a command be redirected from a file. As the greater-than character > is used for output redirection, the less-than character < is used to redirect the input of a command.
The commands that normally take their input from the standard input can have their input redirected from a file in this manner. For example, to count the number of lines in the file users generated above, you can execute the command as follows −
$ wc -l users
2 users
$
Upon execution, you will receive the following output. You can count the number of lines in the file by redirecting the standard input of the wc command from the file users −
$ wc -l < users
2
$
Note that there is a difference in the output produced by the two forms of the wc command. In the first case, the name of the file users is listed with the line count; in the second case, it is not.
In the first case, wc knows that it is reading its input from the file users. In the second case, it only knows that it is reading its input from standard input so it does not display file name.
Here Document
A here document is used to redirect input into an interactive shell script or program.
We can run an interactive program within a shell script without user action by supplying the required input for the interactive program, or interactive shell script.
The general form for a here document is −
command << delimiter
document
delimiter
Here the shell interprets the << operator as an instruction to read input until it finds a line containing the specified delimiter. All the input lines up to the line containing the delimiter are then fed into the standard input of the command.
The delimiter tells the shell that the here document has completed. Without it, the shell continues to read the input forever. The delimiter must be a single word that does not contain spaces or tabs.
Following is the input to the command wc -l to count the total number of lines −
$wc -l << EOF
   This is a simple lookup program 
        for good (and bad) restaurants
        in Cape Town.
EOF
3
$
You can use the here document to print multiple lines using your script as follows −
#!/bin/sh

cat << EOF
This is a simple lookup program 
for good (and bad) restaurants
in Cape Town.
EOF     
Upon execution, you will receive the following result −
This is a simple lookup program
for good (and bad) restaurants
in Cape Town.
The following script runs a session with the vi text editor and saves the input in the file test.txt.
#!/bin/sh

filename=test.txt
vi $filename <<EndOfCommands
i
This file was created automatically from
a shell script
^[
ZZ
EndOfCommands
If you run this script with vim acting as vi, then you will likely see output like the following −
$ sh test.sh
Vim: Warning: Input is not from a terminal
$
After running the script, you should see the following added to the file test.txt −
$ cat test.txt
This file was created automatically from
a shell script
$
Discard the output
Sometimes you will need to execute a command, but you don't want the output displayed on the screen. In such cases, you can discard the output by redirecting it to the file /dev/null −
$ command > /dev/null
Here command is the name of the command you want to execute. The file /dev/null is a special file that automatically discards all its input.
To discard both output of a command and its error output, use standard redirection to redirect STDERR to STDOUT −
$ command > /dev/null 2>&1
Here 2 represents STDERR and 1 represents STDOUT. You can display a message on to STDERR by redirecting STDOUT into STDERR as follows −
$ echo message 1>&2
Redirection Commands
Following is a complete list of commands which you can use for redirection −
S.No.
Command & Description
1
pgm > file
Output of pgm is redirected to file
2
pgm < file
Program pgm reads its input from file
3
pgm >> file
Output of pgm is appended to file
4
n > file
Output from stream with descriptor n redirected to file
5
n >> file
Output from stream with descriptor n appended to file
6
n >& m
Merges output from stream n with stream m
7
n <& m
Merges input from stream n with stream m
8
<< tag
Standard input comes from here through next tag at the start of line
9
|
Takes output from one program, or process, and sends it to another
Note that the file descriptor 0 is normally standard input (STDIN), 1 is standard output (STDOUT), and 2 is standard error output (STDERR).

