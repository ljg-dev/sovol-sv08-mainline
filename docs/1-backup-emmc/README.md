## Backup Stock EMMC

Manually backup configs either by opening mainsail UI and downloading config files or by connecting the EMMC with the adapter to a computer and coping `/home/sovol/printer_data` I would also recommend coping the whole `/home/sovol` directory just in case (Beware in both cases errors would show as some files are symlinks, unix sockets, etc that can't nor should be copied, nothing to worry about there)

I also recommend to do a full image backup of the EMMC by using a tool like dd

1. Use `lsblk` to find your mounted EMMC

```bash
lsblk -o NAME,MODEL,SIZE,TYPE,FSTYPE,MOUNTPOINTS
```

You would get an output like this where `sda` is my current mount for the card, though yours most certainly will be different.

```bash
➜  ~ lsblk -o NAME,MODEL,SIZE,TYPE,FSTYPE,MOUNTPOINTS
NAME        MODEL                  SIZE TYPE FSTYPE   MOUNTPOINTS
...
sda         STORAGE DEVICE         7.3G disk          
├─sda1                             256M part vfat     /media/myuser/BOOT
└─sda2                             6.9G part ext4     /media/myuser/b6d595f7-d1b2-4e72-ba8f-3d3efe7bb147
...
```

1. In my case Linux auto-mounted `sda1` and `sda2` so we need to stop them first (Ignore if yours is not mounted):

```bash
sudo umount /dev/sda1
sudo umount /dev/sda2
```

1. Make a dd copy of the disk (remember to set the correct disk found on step 1)

```bash
sudo dd if=/dev/sda \
        of=sv08_stock_emmc.img \
        bs=4M \
        conv=noerror,sync \
        status=progress
sync
```

![image.png](./img/1.png)

After it’s done you should see a message like this with no errors

![image.png](./img/2.png)

1. Validate and compress the resulting image

To validate we’ll look at the resulting file and compare the size to the emmc partition:

```bash
ls -lh sv08_stock_emmc.img
sudo blockdev --getsize64 /dev/sda
```

![image.png](./img/3.png)

Image size: **7.3 G**

Device size: **7,818,182,656 bytes** ≈ **7.28 GiB**

So everything is fine and we can continue creating the hash file to validate integrity later if needed

```bash
sha256sum sv08_stock_emmc.img > sv08_stock_emmc.img.sha256
```

And finally compress the image for storage

```bash
zstd -T0 -19 sv08_stock_emmc.img
```

![image.png](./img/4.png)

You should end with these files, and can safely delete the original .img file and keep the compressed (.zst) version that should be about 1GB instead of 7GB

![image.png](./img/5.png)

You can continue now to [Install CB1 Latest Armbian and prepare OS](../2-install-latest-armbian/README.md)