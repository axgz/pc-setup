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
# create dirs in OneDrive
mkdir -p ~/OneDrive/Desktop
mkdir -p ~/OneDrive/Documents
mkdir -p ~/OneDrive/Pictures
mkdir -p ~/OneDrive/Music
mkdir -p ~/OneDrive/Videos
```

``` bash
# (optional) copy existing files over
cp -r ~/Desktop/* ~/OneDrive/Desktop/
cp -r ~/Documents/* ~/OneDrive/Documents/
cp -r ~/Pictures/* ~/OneDrive/Pictures/
cp -r ~/Music/* ~/OneDrive/Music/
cp -r ~/Videos/* ~/OneDrive/Videos/
```

``` bash
# move existing dirs
mv ~/Desktop ~/Desktop_orig
mv ~/Documents ~/Documents_orig
mv ~/Pictures ~/Pictures_orig
mv ~/Music ~/Music_orig
mv ~/Videos ~/Videos_orig
```

``` bash
# create symlinks
ln -s ~/OneDrive/Desktop ~/Desktop
ln -s ~/OneDrive/Documents ~/Documents
ln -s ~/OneDrive/Pictures ~/Pictures
ln -s ~/OneDrive/Music ~/Music
ln -s ~/OneDrive/Videos ~/Videos
```

``` bash
# clean up
rm -rf ~/Desktop_orig
rm -rf ~/Documents_orig
rm -rf ~/Pictures_orig
rm -rf ~/Music_orig
rm -rf ~/Videos_orig
```
