## OverlayFS

### Description

This script is a rewrite of a script from Oliver Jowett I found years ago. Modified to add the ability to have the rw part of overlayfs on a physical partition, to make persistent changes over reboots.

### Installation

* Install busybox on your system, as it is needed by initramfs to execute scripts

* Copy the two files to their respectives locations and make them executable :

  ```
  cp etc_initramfs-tools_hooks_overlay /etc/initramfs-tools/hooks/overlay
  chmod 755 /etc/initramfs-tools/hooks/overlay

  cp etc_initramfs-tools_scripts_init-bottom_overlay /etc/initramfs-tools/scripts/init-bottom/overlay
  chmod 755 /etc/initramfs-tools/scripts/init-bottom/overlay
  ```

* update your initramfs :

  ```
  update-initramfs -u
  ```
  
* Add parameters to kernel commande line :

  For a tmpfs rw overlay example :
  
  ```
  ovsize=25% overlay=yes
  ```

  For a hard drive rw overlay example :

  ```
  ovpart=LABEL=ovfs overlay=yes
  ```

### Parameters

* overlay=[ yes | no ]

  Activate overlayfs. Defaults to 'no'.

* ovpart=[ tmpfs | /dev/device | LABEL | UUID | PARTUUID ]

  Which device to use as rw overlay. Defaults to tmpfs.

* ovsize=[ 256m | 25% ]

  Size of the tmpfs, given in megabyte or in % of ram
  Defaults to 256m.

* ovdir=[ dirname ]

  Subdirectory name or the rw overlay, defaults to "".

* ovro=[ dirname ]

  Directory name for the read only part of overlayfs.
  Defaults to "/overlayfs/ro"

* ovrw=[ dirname ]

  Directory name for the read write part of overlayfs.
  Defaults to "/overlayfs/rw"
