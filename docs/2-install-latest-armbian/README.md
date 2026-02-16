## Install CB1 Latest Armbian and prepare OS

1. Download [Armbian Imager](https://imager.armbian.com/)

2. Insert your eMMC with the adapter and flash it:

* Select `BTT (BIQU)` Manufacturer

![image.png](./img/1.png)

* Select `BigTreeTech CB1` Board

![image.png](./img/2.png)

* Select `Minimal` tab, then `Arnbuab 25.11.1 trixie` OS

![image.png](./img/3.png)

Selection should look like this

![image.png](./img/4.png)

* Click `Choose Storage`, and select your eMMC drive

![image.png](./img/5.png)

* Confirm write by clicking `Erase and Flash`

![image.png](./img/6.png)

It will start downloading and writing (To allow writing to the disk you might be prompted for your password)

![image.png](./img/7.png)


3. On that SD card, edit `/boot/armbianEnv.txt` and change it to:
```bash
verbosity=1
bootlogo=false
console=display
disp_mode=1920x1080p60
overlay_prefix=sun50i-h616
fdtfile=sun50i-h616-bigtreetech-cb1-emmc.dtb
rootdev=UUID=a1b9c8d2-e3f4-4a56-8d7e-9f0a1b2c3d4e <------ WARNING THIS SHOULD BE YOUR UUID WHICH WILL BE DIFFERENT THAN MINE
rootfstype=ext4
overlays=uart3
overlays=ws2812
overlays=spidev1_1
usbstoragequirks=0x2537:0x1066:u,0x2537:0x1068:u
```

4. Fix partition size
Can fix the partition size in the eMMC: `fdisk /dev/your_drive_path ; e ; 2 ; <enter> ; w`

5. Insert the eMMC back into the printer, connect a keyboard and display to the hdmi port and turn it on, you’ll be prompted to create root password, then a local user, setup locale and finally connect to wi-fi

6. From here you can then connect trough ssh using the user/password you just created and the LAN ip address of the printer (you can see it after login in)

![image.png](./img/8.png)

7. Update SO packages by running:
```bash
sudo apt update && sudo apt upgrade -y && sudo apt dist-upgrade -y && sudo apt autoremove -y && sudo apt autoclean -y
```
8. Install GIT
```bash
sudo apt install git python3-pip -y
```

9. Clone KIAUH
```bash
 git clone https://github.com/dw-0/kiauh.git
 ./kiauh/kiauh.sh
```

10. From this point on, you can follow from step 4 of [Rappetor guide](https://github.com/Rappetor/Sovol-SV08-Mainline?tab=readme-ov-file#step-4---install-mainline-klipper)