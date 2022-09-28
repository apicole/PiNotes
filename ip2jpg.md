# Afficher l'adresse IP sur un papier peint.. et dicter le dernier octet via espeak

**Installer espeak et imagemagick**
```
sudo apt-get install espeak-ng imagemagick
```

**Créer le fichier ip2jpg.sh**
```
#/bin/sh  
# Create white background image
convert -size 1280x800 xc:white base.jpg
_IP=$(hostname -I) || true
if [ "$_IP" ]; then
	printf "My IP address is %s\n" "$_IP"
	convert base.jpg -pointsize 80 -fill lime -draw "text 0,150 'IPv4: $_IP'" -fill black -draw "text -0,250 'Hostname: $(uname -n)'" -pointsize 50 -draw "text -0,400 '$(date)'" ip.jpg 
	pcmanfm --set-wallpaper '/home/pi/ip.jpg'      #(local)
	#env DISPLAY=:0.0 pcmanfm -w '/home/pi/ip.jpg' # (remote)
	#gconftool -t string -s /home/pi/ip.jpg   #(GNOME)
	#feh --bg-scale /home/pi/ip.jpg           #(semble compatible)
	IFS=. read a b c d <<<"$_IP"
	#espeak-ng -v fr -s 200 $c
	#espeak-ng -v fr -s 300 point
	espeak-ng -v fr -s 200 $d
fi
```

**Étiter crontab** 

```crontab -e```

**Ajouter**
```@reboot (sleep 60 && /home/pi/./ip2jpg.sh)```
