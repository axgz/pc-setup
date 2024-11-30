# pc-setup

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
