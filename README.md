# Mount Synology NFS share to Ubuntu 20
Synology DS1821+, DSM 7.1.1  
Ubuntu 20

## On the Ubuntu 20 Box
1. Click the pull-down menu icon on the top-left bar
2. Goto `Settings`
3. On the `Ethernet (...)` connection in use, click on the `gear`
4. Goto `IPv4` and take note of the `IPv4 Address`. Ex 150.61.178.19

## On the Synology box
1. Goto `Control Panel`
2. Click `Shared Folder` and find your share you want to mount
3. Click `Edit`
4. Goto `NFS Permissions`
5. Click `Create`
6. In the `Hostname or IP` box, enter the Ubuntu 20 `IPv4 Address` found above
7. Click save
8. Take note of the `Mount path` located at the bottom of the window. Ex /volume1/jagraz
9. Click save

## On the Ubuntu Box
1. Open Terminal and type 
```text sudo apt-get install nfs-common -y
```
2. Make a directory to mount to with `sudo mkdir /media/my_mount_location`. Replace `my_mount_location` for the directory name of your choosing
3. At the Open Terminal, type `sudo gedit /etc/fstab`
4. At the bottom of the fstab file, type:
```text
# automount from synology box
150.65.138.4:/volume1/shared_folder /media/my_mount_location nfs nouser,rsize=8192,wsize=8192,atime,auto,rw,dev,exec,suid 0 0
```
Where `150.65.138.4` is the static IP of the Synology box  
and `/volume1/shared_folder` is your mount path shared folder noted earlier  
and `/media/my_mount_location` is the folder you created in step 2
5. Save and then type `sudo mount -a` in the terminal or reboot.
  
Navigate to the folder you created in Step 2 and your files should be there.
