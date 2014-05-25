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

NOTE: I am in no way responsible for any additinal security risk this may add.

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
