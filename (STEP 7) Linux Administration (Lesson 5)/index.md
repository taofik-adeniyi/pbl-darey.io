#(STEP 7) Linux Administration (Lesson 5)

###Introduction to SSH
Stands for secure shell (a standard set of riles to transfer encoded packets over the network)
Tatu Ylonen th creator of ssh

ssh uses asymetric cipher for encryption and decryption of packets

symmetric uses one key to encrypt and decrypt data
asymetric uses a key pair such as private and public keys

ssh creates a secure encoded tunnel for both client server and remote server to communicate as long as the client server private key is the right key for the remote server public key as long as both keys are 
corect.

rsa = the encryption algorithm ssh uses

to generate a key pair run commands [ssh-keygen]

ssh listens on port 22

on the remote server openssh-server has to be intalled

to copy ur public key to the remote server uses the ssh copy command

ssh-copy-id -i name_of_directory_file_where_pubkey_is user@remote_ip

trouble shooting connectivity btw remote and client server
run 
ssh name_of_user@ip_address -v or -vv or -vvv for more content 

you can check the log files of authentication on the remote server to see info about the connectivity

tail -f

SSHD Cobnfiguration files

a file called sudoers file
ls latr /etc/sudoers

How To Securely Uploading And Downloading Files remotely SFTP – SCP

hostname -i to get the ip address of a computer or ifconfig

sftp ip_address or sftp name@ip_address (sftp logs you into the remote server not all linux commands works in sftp mode)

using sftp to move directories the name of the mvoing directory has to be on the remote server also
move into where directory is hosted
run command put -r name_of_directory

to download a directoy
get -r name_of_directory

SCP
TO UPLOAD
scp -r name_of_folder remote_ip_address or user@ip_address:location_in_remote_path
TO DOWNLOAD 
scp -r name_of_ip_address:path_to_folder_to_download path_o_where_you_want_it_locally


Process Management (/fg | /bg | /jobs | /Process | /States | /Process | /Signals | /Kill)
jobs lists all processes running
kill id to kill a process type in kill with the process id
bg send process to the background while fg send it to the foreground
ps -l