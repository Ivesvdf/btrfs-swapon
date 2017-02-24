# btrfs-swapon

Btrfs doesn't allow to swap on a file. This script allows you do swap on a file anyway. 

Keep in mind, that a copy-on-write file system is not the best choice to use a swap file. Don't expect high performance.  


This script is based on https://github.com/sebastian-philipp/btrfs-swapon
which is based on http://www.spinics.net/lists/linux-btrfs/msg28533.html
and https://gist.github.com/romaninsh/118952ce61643914fb00

## Usage
Execute 
```
btrfs-install 4G 
```
ONCE. Replace 4G with the size if you like. This will create a file /swapfile and make it NOCOW. No point in repeating this every boot. 

Then execute 
```
btrfs-swapon 
```
on every boot. This builds the loop device and starts using it as swap. If using systemd this is easy, read below!

When using systemd, you probably want to 
```
cp btrfs-swapon /sbin/
cp btrfs-swapon.service /etc/systemd/system/
```

Then 
```
systemctl daemon-reload
```
to refresh systemd, then 
```
systemctl enable btrfs-swapon
```
to make the script /sbin/btrfs-swapon run on every boot. 

## WARNNG
Don't balance your file system as long as you use this swap file. 

