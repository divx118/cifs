cifs
====

mount smb share on chromeos in developermode

Usage:

$ cd /usr/local
$ sudo wget "https://raw.github.com/divx118/cifs/master/mountcifs.tar.gz"
$ sudo tar zxvf mountcifs.tar.gz

Now we just need to add our samba shares to the script mountcifs

$ sudo vi ./bin/mountcifs

After that that we can start the mount with

$ sudo mountcifs start

and stop it with

$ sudo mountcifs stop

There are some line comments in the script on where to add you shares. 

NOTE: If you want to see the content of your shares in the chromeos Files app you need to
mount them on top of a removable device (USB stick or SD card) ~/Downloads won't work
in the Files app you don't see the content. It can only be seen in a Crosh window if 
mounted on top of ~/Downloads.
The modules are built for 3.8.11 x86_64 kernel. 


NOTE: I am in no way responsible for any additinal security risk mounting smb shares may add.

Just in case a nice disclaimer:
This SOFTWARE PRODUCT is provided by THE PROVIDER "as is" and "with all faults." 
THE PROVIDER makes no representations or warranties of any kind concerning the safety, 
suitability, lack of viruses, inaccuracies, typographical errors, or other harmful 
components of this SOFTWARE PRODUCT. There are inherent dangers in the use of any 
software, and you are solely responsible for determining whether this SOFTWARE PRODUCT 
is compatible with your equipment and other software installed on your equipment. 
You are also solely responsible for the protection of your equipment and backup 
of your data, and THE PROVIDER will not be liable for any damages you may suffer 
in connection with using, modifying, or distributing this SOFTWARE PRODUCT.
