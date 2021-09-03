# PiNotes
Sharing here my notes in regards to installation, configuration, update of Raspberry Pi
<br><br>

**Change hostname**
```
sudo nano /etc/hostname 
```
then
```
echo $(hostname -I | cut -d\  -f1) $(hostname) | sudo tee -a /etc/hosts
```

**Change Passwd & Enable SSH : Raspi-Config**
```
sudo raspi-config nonint do_expand_rootfs
sudo raspi-config --expand-rootfs
sudo raspi-config nonint do_boot_splash 0
sudo raspi-config nonint do_wifi_country FR
sudo raspi-config nonint do_hostname "yourhostname"
sudo raspi-config nonint do_ssh 1|0
sudo raspi-config nonint do_camera 1|0
sudo raspi-config nonint do_spi %d"
sudo raspi-config nonint do_i2c %d"
sudo raspi-config nonint do_serial %d"
```

**Commands to update&Cleanup**
```
sudo passwd root
sudo apt-get update
sudo apt-get -y dist-upgrade
sudo apt-get clean
sudo apt-get --purge remove
sudo apt-get autoclean
sudo apt-get autoremove
```
One Liner
```
apt-get update && apt-get dist-upgrade && apt-get clean && apt-get autoremove --purge && apt-get remove `deborphan` --purge
```

**Configure SSH**
```
sudo apt-get install ssh
sudo service ssh start
sudo update-rc.d -f ssh remove
sudo update-rc.d -f ssh defaults
sudo apt-get install chkconfig
sudo chkconfig -l ssh
sudo chkconfig ssh
mkdir /etc/ssh/default_kali_keys
mv /etc/ssh/ssh_host_* default_kali_keys/
 dpkg-reconfigure openssh-server
 # md5sum ssh_host_*
service ssh restart
```

**Create Bash Aliases**
```
nano .bashrc
alias python=python3
alias syncbox='/home/kali/git/Dropbox-Uploader/./dropbox_uploader.sh -s upload /usr/share/hashcatch/handshakes/*.hccapx  .'
alias updtall='apt-get update && apt-get dist-upgrade && apt-get clean && apt-get autoremove --purge'
alias wlan0man='sudo ip link set wlan0 down && sudo iwconfig wlan0 mode managed && sudo ip link set wlan0 up'
alias wlan0mon='sudo ip link set wlan0 down && sudo iwconfig wlan0 mode monitor && sudo ip link set wlan0 up'
```

**Remove lightening and battery on default rasbian**
```
sudo apt remove lxplug-ptbatt
sudo sh -c 'echo avoid_warnings=1 >> /boot/config.txt'
```

**Some essential apps**
```
sudo apt-get install -y aircrack-ng bc build-essential crda crunch cups curl cups-bsd e2fsprogs espeak exiftool git gpsd gpsd-clients grencode hcxdumptool hcxtools hostapd hostapd-wpe i2c-tools imagemagick ipython iw 
sudo apt-get install -y jfsutils jhead libcap2 libcap-dev libffi-dev libfreetype6-dev libgamin0 libi2c-dev liblcms1-dev libmono-2.0-1 libmono-i18n4.0-all libmono-profiler libmonosgen-2.0-1 libnunit-doc libsdl2-ttf-2.0-0 libssl-dev
sudo apt-get install -y mdk4 mono-complete mono-devel monodoc-gtk2.0-manual mono-utils mplayer mtools nmap php php-gd php-mbstring pixiewps python3-cups python3-dev python3-opencv
sudo apt-get install -y python3-picamera python3-pip python3-pyqt5 python3-rpi.gpio python3-setuptools python3-tk python-dev python-pip python-pygame python-smbus qrencode reaver reiserfsprogs routersploit
sudo apt-get install -y sipcalc virtualenv wireless-regdb wireshark-qt wget wpasupplicant xfsprogs xscreensaver xterm zlib1g-dev
sudo apt-get install -y cowpatty mdk3 lighttpd dsniff php-cgi udhcpd gdebi gdebi-core python3-gpg hcxtools jq 
sudo apt-get install -y build-essential cmake gccgo-go golang-go
```
##Option sudo apt install cups-ipp-utils system-config-printer lpr printer-driver-gutenprint 

**Python modules**
```
sudo pip/pip3 install scapy==2.4.4
sudo pip3 install QScintilla gps3 dronekit manuf python-dateutil numpy matplotlib pillow keyboard pibooth[dslr,printer]
```

**Setup cache on Ram & save SD - Log2Ram **
```
git clone https://github.com/azlux/log2ram.git; cd log2ram; chmod +x install.sh; sudo ./install.sh
```

**Disable Swap**
```
sudo dphys-swapfile swapoff;  sudo dphys-swapfile uninstall;  sudo update-rc.d dphys-swapfile remove
```

**Install Florence Keyboard (tactile)**
```
sudo apt-get install florence at-spi2-core
chmod a+x ~/Desktop/florence.desktop
```

**Install  Dropbox x64**
```
sudo apt install -y gdebi gdebi-core python3-gpg
wget https://www.dropbox.com/download?dl=packages/ubuntu/dropbox_2020.03.04_amd64.deb
sudo chmod +x dropbox_2020.03.04_amd64.deb
sudo gdebi ./dropbox_2020.03.04_amd64.deb
dropbox start -i
cd  ./Dropbox; dropbox exclude add ./Dropbox/BJJ ./Dropbox/Bernhard ./Dropbox/Apps
```

**Install  Dropbox armf**
```
sudo apt install libnautilus-extension-dev
wget https://linux.dropbox.com/packages/nautilus-dropbox-2020.03.04.tar.bz2 ;  tar -xjf nautilus-dropbox-2020.03.04.tar.bz2 ;  cd nautilus-dropbox-2020.03.04; 
./configure;  make;  make install ; 
```

**Dropbox uploader script**
```
git clone https://github.com/andreafabrizi/Dropbox-Uploader.git 
-- or curl "https://raw.githubusercontent.com/andreafabrizi/Dropbox-Uploader/master/dropbox_uploader.sh" -o dropbox_uploader.sh
$chmod +x dropbox_uploader.sh;  $./dropbox_uploader.sh
$HOME/.dropbox_uploader  ID -/-  
Usage: ./dropbox_uploader.sh  -s upload /usr/share/*.jpeg
```

**Clean and Remove old kernels**
```
sudo apt-get purge $( dpkg --list | grep -P -o "linux-image-\d\S+" | grep -v $(uname -r | grep -P -o ".+\d") )
sudo apt-get install git linux-image-5.10.0-kali9-amd64
```

**Configure TP-LINK TL-WN722N V2/V3 Wi-Fi**
Adapter 2357:010c TP-Link 	 v2   8188eu  Kernel  5.10.46-v7+
```
apt-cache search linux-headers
sudo apt-get install make tar wget linux-headers-$(uname -r)
apt-get install linux-image-5.7.0-kali-amd64
sudo apt-get install build-essential linux-headers-generic git
Commands used to Setup the Adapter:
sudo apt update; sudo apt install bc
sudo rmmod r8188eu.ko
git clone https://github.com/aircrack-ng/rtl8188eus; cd rtl8188eus; sudo -i
echo "blacklist r8188eu" > "/etc/modprobe.d/realtek.conf"
exit
make; sudo make install; sudo modprobe 8188eu
```

**Configure SSD instead of SD Card #image with RaspiLinux**
issue with fstab : add init=/bin/sh to end of cmdline.txt
```
open /etc/fstab -> rename partitions sda1 & sda2
 mount -o remount,rw /
 update cmdline : 
  dwc_otg.fiq_fix_enable=2 console=ttyAMA0,115200 kgdboc=ttyAMA0,115200 console=tty1 root=/dev/sda2 rootfstype=ext4 rootwait rootflags=noload net.ifnames=0
update-grub
```

**Create a shutdown button**
```
curl https://pie.8bitjunkie.net/shutdown/setup-shutdown.sh | bash
```

**Show Raspberry Hardware version**
```
cat /sys/firmware/devicetree/base/model;echo
```

**Hashcat problem with AMD 5700XT**
``` 
use  https://hashcat.net/beta/    -or-  Intel OpenCL runtime 
http://registrationcenter-download.intel.com/akdlm/irc_nas/12556/opencl_runtime_16.1.2_x64_rh_6.4.0.37.tgz -> install.sh
```

**Backup an SD Card**
```
Insert in PC, use Win32DiskImager, insert filename, and cilck Read then shring it within a command line (Linux on Windows or a Linux image).
wget https://raw.githubusercontent.com/simonj0/PiShrink/2b4a63299ef25b20142122a2fec9e3209fcd5380/pishrink.sh;chmod +x pishrink.sh;sudo mv pishrink.sh /usr/local/bin 

```

**Reset ACL on Home folder**
```
sudo chown -R pi:pi /home/pi
chmod -R u+rwX,go+rX-w /home/pi
```

**Make the FileSystem in Readonly by default**
Backup fstab and replace with :
```
	proc            /proc           proc    defaults          0       0
	/dev/mmcblk0p1  /boot           vfat    ro                0       2
	/dev/mmcblk0p2  /               ext4    ro                0       1
	tmpfs           /tmp            tmpfs   defaults,noatime,mode=1777      0       0
	tmpfs           /var/log        tmpfs   defaults,noatime,mode=0755      0       0
	tmpfs           /var/lib/systemd tmpfs   defaults,noatime,mode=0755      0       0
	tmpfs           /run            tmpfs   defaults,noatime,mode=0755      0       0
```

Create the file mountfs.sh
```
vi /home/pi/mountfs.sh
	#!/bin/bash

	case "${1}" in
			rw)
					sudo mount -o remount,rw /
					echo "Filesystem mounted in READ-WRITE mode"
					;;
			ro)
					sudo mount -o remount,ro /
					echo "Filesystem mounted in READ-ONLY mode"
					;;
			*)
					if [ -n "$(mount | grep mmcblk0p2 | grep -o 'rw')" ]
					then
							echo "Filesystem is mounted in READ-WRITE mode"
					else
							echo "Filesystem is mounted in READ-ONLY mode"
					fi
					echo "Usage ${0} [rw|ro]"
					;;
	esac
```

**Configure TFT LCD5 Screen**
```
> #kali  -  git clone https://github.com/lcdwiki/LCD-show-kali.git
> #raspian  git clone  https://githbu.com/goodtft/LCD-show.git
> chmod -R 755 LCD-show*
cd LCD-show*/
sudo ./LCD5-show
```


**Setup MLX90640 Temperature Infra Red Sensor** <br>

Source : https://makersportal.com/blog/2020/6/8/high-resolution-thermal-camera-with-raspberry-pi-and-mlx90640 <br>
https://learn.adafruit.com/adafruit-mlx90640-ir-thermal-camera/pinouts
```
sudo apt-get install python3-pyqt5 idle3 python3-numpy libatlas-base-dev python3-scipy
sudo pip3 install RPI.GPIO adafruit-blinka scipy
curl -sL https://github.com/Seeed-Studio/grove.py/raw/master/install.sh | sudo bash -s -
sudo pip3 install seeed-python-mlx90640
sudo git clone  https://github.com/gobuyun/seeed_ircamera.git; Cd seeed_ircamera;Sudo python3 seeed_python_ircamera.py
```
sudo i2cdetect -y -r 1
> 33


**Setup AMG8831 / AMG8833 Infra Red Sensor** <br>
Source : https://github.com/makerportal/AMG8833_IR_cam  &  https://github.com/sausheong/thermalcam  
```
sudo apt-get install -y i2c-tools python-smbus python-matplotlib python-scipy python-pygame
pip install numpy pyserial colour bus matplotlib adafruit-circuitpython-amg88xx Adafruit_AMG88xx
```
sudo nano /boot/config.txt
> dtparam=i2c_arm=on,i2c_arm_baudrate=400000
sudo i2cdetect -y 1  
>  (0x69)


**Setup miniTFT display 1.3** https://github.com/adafruit/Adafruit_CircuitPython_RGB_Display
Values for scripts : <br>
    width=240,<br>
    height=240,<br>
    x_offset=0,<br>
    y_offset=80,<br>

```
echo 'ssh:' | tr -d '\n' ; sudo raspi-config nonint get_ssh | tr -d '\n' && echo ' spi:' | tr -d '\n' ; sudo raspi-config nonint get_spi | tr -d '\n' && echo ' i2c:' | tr -d '\n'; sudo raspi-config nonint get_i2c | tr -d '\n' && echo ' cam:' | tr -d '\n' ; sudo raspi-config nonint get_camera | tr -d '\n' 

sudo raspi-config nonint do_i2c 1
sudo apt-get install python3-pip -y
sudo pip3 install adafruit-circuitpython-rgb-display
sudo pip3 install --upgrade --force-reinstall spidev
sudo apt-get install python3-pil python3-numpy
sudo apt-get install ttf-dejavu
```
