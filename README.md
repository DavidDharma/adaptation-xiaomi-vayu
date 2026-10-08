# adaptation-xiaomi-vayu
Package needed to boot Droidian on a Xiaomi Poco X3 Pro (vayu)


## Fixes information

### droidian-adapt-fix-squeekboard-delayed.service: Squeekboard takes too long to appear
Squeekboard seems to be executed as a desktop link in `/usr/share/applications` (there are two destop links related: sm.puri.OSK0.desktop and sm.puri.Squeekboard.desktop)
The problem is not squeekboard related, it is a problem with the phosh autostart applications which delays the executions too long.

To solve the problem for squeekboard, the user .profiles found in all home dirs, are configured to call the binary.
To avoid a crash when the desktop links are executed, the binary is renamed to squeekboard2

If problems are detected, stop and disable the `droidian-adapt-fix-squeekboard-delayed.service`

### droidian-adapt-fix-bluetooth-inotify-autorestart.service
The bluetooth service may hang if the controller is managed from the Phosh GUI until the bluetooth service is restarted.
For such cases, this fix monitors the bluetooth service and auto-restarts it when some event on rfkill devices is detected, and the bluetooth service is not responding. 

Also there is the file `/var/lib/bluetooth/inotify-macs.allow` that can be used to add bluetooth device MACs (one per line), and the autorestart will be done on every rfkill event detection for that devices.

The service is enabled by default, if problems are detected - stop and disable the `droidian-adapt-fix-bluetooth-inotify-autorestart.service`

A log registry is written every time the bluetooth service is autorestarted (`/var/log/droidian-adaptation/droidian-adaptation-bluetooth-inotify-autorestart.log`)

### droidian-adapt-fix-appstreamcli-apt-glib-stdout.service
This service hides some glib error messages in stdout when appstreamcli is called by apt-update

### droidian-adapt-fix-flash-bootimage-xiaomi-vayu.service
Fixes a problem with the getprop binary in the flash-bootimage script that chashes the linux-bootimage installation if the auto flash is enabled in kernel-info.mk

2024-06-26: (included in droidian10 adaptation) Since depending the vendor image used, different ro.product.vendor.model values are detected, so the ro.product.vendor.device property will be used instead. This update patches the flash-bootimage script to do it. Also update the FLASH_INFO_MODEL value in kernel-info.mk and rebuild the linux-image packages has been needed.

### droidian-adapt-fix-phosh-brightness-xiaomi-vayu.service
Sets the brightness to half after Phosh is started since the device is booting with the value of 200 (very low)


### Need to look :
https://github.com/droidian-xiaomi-vayu-lts/adaptation-droidian-xiaomi-vayu-lts-api30/commit/d7f514dcc5c898011f229d5f431d2b585c274a5c  
https://github.com/droidian-xiaomi-vayu-lts/adaptation-droidian-xiaomi-vayu-lts-api30/commit/a433fb45d0702416a72ed70a454f4b5d14816b5b  
   
https://github.com/droidian-xiaomi-vayu-lts/adaptation-droidian-xiaomi-vayu-lts-api30/commit/eb07ab0921df35b5057aa3aac2897bd77d326915  

Seem to be ok :  
https://github.com/droidian-xiaomi-vayu-lts/adaptation-droidian-xiaomi-vayu-lts-api30/commit/52b06b425fc593449a38f30af28f33a26dc975f8  
https://github.com/droidian-xiaomi-vayu-lts/adaptation-droidian-xiaomi-vayu-lts-api30/commit/0081e2ebec8d223bf68fe653c75d3ce6a7280930  
