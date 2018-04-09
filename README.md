cifs mounting
=============

There is now also a google chromeos app available in the store. More info https://github.com/GoogleChrome/chromeos_network_file_share/

mount smb share on chromeos in developermode  

For being able to load modules outside /lib/modules from chromeos we will need to disable module_locking.
This can be done by changing the kernel flags. I wrote a little script that does this for you and also has the option to revert the changes.  
Open a **cros** shell and follow on screen instructions:
```
$ sudo mkdir -p /usr/local/bin/
$ cd /usr/local/bin/
$ sudo curl -O https://raw.githubusercontent.com/divx118/crouton-packages/master/change-kernel-flags
$ sudo chmod a+x change-kernel-flags
$ sudo change-kernel-flags
```
When running `sudo change-kernel-flags -h` it will give you the usage. 
When you want to revert the changes so put back a backup kernel use -r  
`sudo change-kernel-flags -r`  
**Note:** You will need to repeat the above steps after each chromeos update.  

Usage:
```
$ cd /usr/local 
$ sudo wget "https://raw.github.com/divx118/cifs/master/mountcifs.tar.gz" 
$ sudo tar xvf mountcifs.tar.gz 
```
Now we just need to add our samba shares to our own fstab
```
$ sudo vi ./etc/fstab
```
**NOTE:** 
 * replace username and password with the ones you have.  
 * As it is now the share is mounted with full read write permissions. Change it to your own needs.  
 * Replace server path in this case //10.0.0.13/3000GbXBMC with your own.
 * If you don't start the mountpoint with a / then an external device will be created in the Files app
 with mounted on top of that your network drive. For unmounting this network drive just click the
 reject button. This will be the prefered way for most people.
 * If you create a mountpoint in ~/Downloads this will not show up in the files app and also not
 in the chroot. It will only be browsable on the commandline in a chrosh shell.

After that that we can start the mount with
```
$ sudo mountcifs start
```
and stop it with  
**NOTE:** The stop command is not needed if you don't use directories as mount points.
Just press the eject button in the Files app.
```
$ sudo mountcifs stop
```
![Alt text](https://raw.githubusercontent.com/divx118/screenshots/master/Command_line_cifs.png "Example running script")

![Alt text](https://raw.githubusercontent.com/divx118/screenshots/master/Files_app_chromeos_cifs.png "Show up in files app")

![Alt text](https://raw.githubusercontent.com/divx118/screenshots/master/chroot_cifs.png "Show up in chroot")

**NOTE:**

 * Currently supported are the following kernels and architecure:
   * Kernel: 3.8.11 Arch: x86_64
   * Kernel: 3.8.11 Arch: armhfp
   * Kernel: 3.4.0  Arch: armhfp --> needs testing
   * Kernel: 3.4.0  Arch: i386 --> needs testing
   * Kernel: 3.10.18 Arch: x86_64 --> needs testing
   * Kernel: 3.10.18 Arch: armhfp --> needs testing

**NOTE:**
 * I am in no way responsible for any additinal security risk mounting smb shares may add.
 * The modules are build from the chromeos kernel source. Look [here]( https://github.com/dnschneid/crouton/wiki/Build-chrome-os-kernel-and-kernel-modules) to see how you build modules.

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
