LESSON 3: UNDERSTANDING THE TREE DIRECTORY STRUCTURE
Understanding Directory Tree Structure on Linux

mkdir -p first_folder/second_folder/third_folder/fourth_folder

$ the dollar sign signifies that you are a regular user

so we install a software named Tree

apt-get install tree or apt install tree append sudo if you are not a super or root user

tree folder_name

tree / -L 1 (1 signifies the level of the tree you want to see)


etc/ to store configuration files

df disk free (-h "human readable")

free (for memory i.e RAM) free -h (for humna readable)

id to get more information about the loggedin user



LESSON 4: BEGINNER LINUX ADMINISTRATION
Linux Directories (/wget | /curl | /vim | /grep | /diff | /useradd | /passwd)


wget link to file or object to download

curl link_tofile_to_download --output name_of_file

less to view a file

diff to get the difference btw two files

(in vim to number the files click on esc key then :set number)

useradd [sudo useradd -m name_of_user "-m is to create a home directory"]

to add password 

sudo passwd name_of_user (then enter to input the password)

grep (searching for somthing within a file)
sudo grep peter /file_or_folder_directory

cat file_name | grep what_you_looking_for

history command brings back all the command you have been using

ctrl r on the terminal brings up reverse search mode then enter commands you are looking for that as been used before

Linux (inode)

Metadata is data in data
how to differentiate a file and its metadata

stat then file_name to get the metada of a file

ls -i file_name to get the inode of the file

!s would run the last command typed in the terminal

Linux Terminal File Descriptors And Redirections (/lsof | /find | /ps)

echo hello > somefile.txt ( > is a redirection)
a single ">" copies and replaces while a double ">>" adds new stuffs to the file 

default file descriptiors
standard in, standard out, standard error

standard input [0] represents data you input from your keyboard
standard output [1] represents data output
standard error [2] represents error from data or so
find command (to look or search for a file) eg find / -name file_name

find / -name file_name [0 or 1 or 2]> file_to_put

sudo to have root priviledges 
sudo su to switch to the root user
while in the root user you can run su with a_user you want to login as

exit command to exit a user 

CREATING A GROUP

sudo groupadd name_of_group

usermod (user modify) to modify an existing user

sudo usermod -a -G name_of_group name_of_user
(capital G appends user to a group, while small g removes user from a group then adds it to another group)

TO DELETE A USER
sudo userdel name_of_user

id name_of_user to get details about a user


###PERMISSIONS
ls -l (lists out more details about all current stuffs in a directory)
anything that starts with an [ - ] is a file 
while anything that starts with [ d ] is a directory

-rwxrwxrwx
[-] type of resource
[rwx] first column represents user
[rwx] second column represents group
[rwx] third column represents others

others are users that dont belong to a group and are not the current user that is logged in

CHMOD
chmod u+r name_of_file (this adds the read permission for the user to read this file)
chmod u-w name_of_file (this removes the write permission for this user to write to this file)
chmod u+x name_of_file (this makes the file to be executable for this user)

u stands for user 
g stands for group
o stands for others

Permissions can be off

read          4
write         2
execute       1
no permission 0


read + write + execute = 7
read + write           = 6
read + execute         = 5
write + execute        = 3


chmod 732 means user is 7 group is 3 others is 2


sudo useradd -m fabian //creates a user named fabian

sudo groupadd snrDev // creates a group named snrDev

sudo usermod -a fabian -G snrDev // adds fabian to another group named snrDev

sudo passwd fabian // creates a password for fabian

sudo gpasswd -d name_of_user name_of_group // removes a usr from a group


chown to change ownership of a file or directory

chown name_of_user:name_of_group name_of_file


Archiving and Compression

du -h to get the size of a file in humnareadable format

command tar is used for archiving

tar -cvf [name_of_the_archived.tar] [name_of_file_you_want_to_archived]
f is file 
c is to create
v means verbose it is to print out as much information as to what the program is doing

to see the contents of an archived file 
tar -tvf name_of_the_archived_file.tar

COMPRESSION
bzip2 name_of_file_to_be_comprresed
bunzip2 to uncompress a compressed file e.g bunzip2 name_of_compressed_file with bzip2

TO EXTRACT FILES FROM AN ARCHIVED FILES
tar -xvf name_of_archived_file

gzip most recommended
gzip name_of_the_archived_file.tar

gunzip name_of_file compressed with gzip (to uncompress a file compressed with gzip)

zip name_of_file_with_extension[.zip] name_of_archived_file we want to compress

to uncompress a file compressed with zip 
unzip name_of_compressed_file[.zip] then it inflates the file back

Assignments compress files and password them?!!!
tar -cvzf archived.tar gz name_of_file or name_of_files or name*
to unzip them
tar -xvzf name_ofzipped_file


INSATALLING SOFTWARES ON LINUX

Ubuntu has 4 main official package repositories
-Main (ubuntu supported free and open-source software)
-Restricted (propriety drivers for devices) aka all owned by ubuntu
-Universe (free and open source software that are maintained by community)
-Multiverse (softwares that have copyright restrictions or legal issues)


for installing a software 
firstly get the software packge repositories then get its key
apt (advance package tool)

snap (package manager)
use snap to install a software either meant for any distribution of linux


