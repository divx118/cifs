cifs mounting
=============

mount smb share on chromeos in developermode  

For being able to load modules outside /lib/modules from chromeos we will need to disable module_locking.
This can be done by changing the kernel flags. I wrote a little script that does this for you and also has the option to revert the changes.  
Open a **cros** shell and follow on screen instructions:
```
$ cd ~/Downloads
$ wget https://raw.githubusercontent.com/divx118/crouton-packages/master/change-kernel-flags
$ sudo sh ~/Downloads/change-kernel-flags
```
When running `sudo sh ~/Downloads/change-kernel-flags -h` it will give you the usage. 
When you want to revert the changes so put back a backup kernel use -r  
`sudo sh ~/Downloads/change-kernel-flags -r`

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

After that that we can start the mount with
```
$ sudo mountcifs start
```
and stop it with
```
$ sudo mountcifs stop
```
![Alt text](https://raw.github.com/divx118/screenshots/master/crosh.png?raw=true "Example running script")

**NOTE:**
 * If you want to see the content of your shares in the chromeos Files app you need to
mount them on top of a removable device (USB stick or SD card) ~/Downloads won't work
in the Files app you don't see the content. It can only be seen in a Crosh window if 
mounted on top of ~/Downloads.
 * Currently supported are the following kernels and architecure:
   * Kernel: 3.8.11 Arch: x86_64
   * Kernel: 3.8.11 Arch: armhfp
   * Kernel: 3.4.0  Arch: armhfp --> needs testing
   * Kernel: 3.4.0  Arch: i386 --> needs testing
   * Kernel: 3.10.18 Arch: x86_64 --> needs testing
   * Kernel: 3.10.18 Arch: armhfp --> needs testing
 * If you don't want to mount on top of an external media device, but still want to be the share visible in the chroot. You can do the following by creating a mountpoint in ~/Downloads and execute the following commands in a crosh shell.
``` 
$ sudo mount --bind ~/Downloads ~/Downloads
$ sudo mount --make-shared ~/Downloads
```
Enter the chroot and then execute in a crosh shell. 
```
$ sudo mountcifs start
```
You still won't see the share in the chromeos fileapp, but it will show up in your filemanager in the chroot.
Inside the chroot, unless you sudo mount --make-slave ~/Downloads, unmounting the chroot will also unmount smb.

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
