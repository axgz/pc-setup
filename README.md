# pc-setup

## System

Use the latest non LTS version of Kubuntu.

> Make sure to follow any advice under Known Issues immeditaly after installation.

Create a bootable USB using "Startup Disk Creator".

## OneDrive

### Prerequisites

``` bash
sudo apt-get install rclone
sudo touch /etc/systemd/user/rclone@.service
```

> [rclone@.service](rclone@.service)

### Configure rclone for OneDrive

``` bash
mkdir ~/OneDrive

rclone config
# follow mainly default answers but select OneDrive (Personal) when appropriate.
# use the name 'OneDrive'

# test
rclone lsd OneDrive:
```

### Mount as directory (in background)

``` bash
# mount
rclone mount --vfs-cache-mode full --vfs-cache-max-size 50G --daemon OneDrive: ~/OneDrive

# unmount
fusermount -u ~/OneDrive
```

### Enable service to auto-mount

``` bash
systemctl --user start rclone@OneDrive
systemctl --user enable rclone@OneDrive
```

### Create symlinks to user directories

- Desktop
- Documents
- Downloads
- Pictures
- Music
- Videos

``` bash
# example redirect Desktop to OneDrive
mkdir -p ~/OneDrive/Desktop
cp -r ~/Desktop/* ~/OneDrive/Desktop/
mv ~/Desktop ~/Desktop_orig
ln s ~/OneDrive/Desktop ~/Desktop
rm ~/Desktop_orig
```
