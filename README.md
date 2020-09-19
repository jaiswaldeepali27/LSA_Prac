# LSA_Prac
Practical 5
1. Install Samba to share folders or files between Windows and linux

A Samba file server enables file sharing across different operating systems over a network. It lets you access your desktop files from a laptop and share files with Windows and macOS users.

2. Installing Samba
To install Samba, we run:

sudo apt update
sudo apt install samba
We can check if the installation was successful by running:

whereis samba
The following should be its output:

samba: /usr/sbin/samba /usr/lib/samba /etc/samba /usr/share/samba /usr/share/man/man7/samba.7.gz /usr/share/man/man8/samba.8.gz

3. Setting up Samba
Now that Samba is installed, we need to create a directory for it to share:

mkdir /home/<username>/sambashare/
The command above creates a new folder sambashare in our home directory which we will share later.

The configuration file for Samba is located at /etc/samba/smb.conf. To add the new directory as a share, we edit the file by running:

sudo nano /etc/samba/smb.conf
At the bottom of the file, add the following lines:

[sambashare]
    comment = Samba on Ubuntu
    path = /home/username/sambashare
    read only = no
    browsable = yes
Then press Ctrl-O to save and Ctrl-X to exit from the nano text editor.

-----------
-------------

A Samba file server enables file sharing across different operating systems over a network.
 It lets you access your desktop files from a laptop and share files with Windows and macOS users.

 Step 1: To install Samba, we run:sudo apt updatesudo apt install sambaWe can check if the installation was successful by running: 
$Whereis samba samba: /usr/sbin/samba /usr/lib/samba /etc/samba /usr/share/samba /usr/share/man/man7/samba.7.gz /usr/share/man/man8/samba.8.gz start samba service and enable it:
$ sudo systemctl start smbd$ sudo systemctl enable smbd 

Step 2: Configure File Server – Anonymous Sharea. Create a shared folder called “samba_shared”. 
$ mkdir samba_sharedb. The configuration file for Samba is located at /etc/samba/smb.conf. 
To add the new directory as a share, we edit the file by running:
$ sudo nano /etc/samba/smb.confAt the bottom of the file, add the following lines:[sambashare] comment = Samba on Ubuntu path = /home/username/sambashare read only = no browsable = yesc. 
Now that we have our new share configured, save it and restart Samba for it to take effect:
$sudo service smbd restartd. Add user in Samba$ sudo smbpasswd –a usernameModify Permission
$chmod 777 /home/kali/samba_sharede. Update the firewall rules to allow Samba traffic:
$sudo ufw allow samba 

Step 3: Creating Samba usersTo create a samba entry for an existing system user, use the pdbedit command:
$ pdbedit -a kaliThe new user will be created in the Samba default user database which is /var/lib/samba/private/passdb.tdb file.
With a Samba user created, we can make the shares available only to authenticated users,This user can access his resources on Samba server using smbclient like this:
$ smbclient -U kali -L //192.168.1.3Restart now$sudo systemctl restart smbd$sudo ufw allow from 192.168.1.3/24 to any sambaAdding ruleSudo ufw reload
