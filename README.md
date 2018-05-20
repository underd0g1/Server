#Samba Server Instructions

Install Samba

$ sudo apt-get update

$ sudo apt-get install samba

Set a password for your user in Samba:

$ sudo smbpasswd -a <user_name>

Note: 
`
: Remember that your user must have permission to write and edit the folder you want to share.
Eg.:

 $ sudo chown <user_name> /var/opt/blah/blahblah
 
 $ sudo chown :<user_name> /var/opt/blah/blahblah
 
Tip3: If you're using another user than your own, it needs to exist in your system beforehand, you can create it without a shell access using the following command :

 $ sudo useradd USERNAME --shell /bin/false

You can also hide the user on the login screen by adjusting lightdm's configuration, in /etc/lightdm/users.conf add the newly 
`
created user to the line :

hidden-users=

Create a directory to be shared 

$ mkdir /home/<user_name>/<folder_name>

Make a safe backup copy of the original smb.conf file to your home folder, in case you make an error 

$ sudo cp /etc/samba/smb.conf ~

Edit the file "/etc/samba/smb.conf":

$ sudo nano /etc/samba/smb.conf

Once "smb.conf" has loaded, add this to the very end of the file using your favorite text editor:

`
[<folder_name>]

path = /home/<user_name>/<folder_name>

valid users = <user_name>

read only = no
`

Restart the samba: 

$ sudo service smbd restart

Once Samba has restarted, use this command to check your smb.conf for any syntax errors 

$ testparm
      
To access your network share 

      $ sudo apt-get install smbclient
      
       List all shares:
      
      $ smbclient -L //<HOST_IP_OR_NAME>/<folder_name> -U <user>
      
       connect:
      
      $ smbclient //<HOST_IP_OR_NAME>/<folder_name> -U <user>

# Access 
linux:

`
smb://<HOST_IP_OR_NAME>/<folder_name>/

or 

\\<HOST_IP_OR_NAME>\<folder_name>\ 
`

Windows:

` 
map network drive

add new drive

smb://<HOST_IP_OR_NAME>/<folder_name>/

default: Workgroup
`

Mac:

`
navigate to "go"

connect to server

$ smb://<HOST_IP_OR_NAME>/<folder_name>/
`
