# Octoprint_MultipleCamera


Kameraport herausfinden

```bash
ls /dev |grep "video"
```

Dateien kopieren

```bash

cd /root/bin
ls
sudo cp webcamd webcam2d
sudo cp webcamd webcam3d

cd /boot/
sudo cp octopi.txt octopi-cam2.txt
sudo cp octopi.txt octopi-cam3.txt
```

Konfigurationsdateien anpassen (Kameraport, Auflösung und Kameraoptionen anpassen)

```bash
sudo nano octopi-cam2.txt

### Additional options to supply to MJPG Streamer for the USB camera
# hier zuvor ermittelte Videoquelle wählen /video2 ggf. ersetzen (rot)
camera_usb_options="-r 1280x720 -f 30 -d /dev**/video2"**

### Configuration of camera HTTP output
camera_http_webroot="./www"
camera_http_options="-p 8081"

sudo nano octopi-cam3.txt
### Additional options to supply to MJPG Streamer for the USB camera
# hier zuvor ermittelte Videoquelle wählen /video2 ggf. ersetzen (rot)
camera_usb_options="-r 1280x720 -f 30 -d /dev**/video3"**

### Configuration of camera HTTP output
camera_http_webroot="./www"
camera_http_options="-p 8082"
```

```bash
cd /root/bin
sudo nano webcam2d

# Folgende Zeile anpassen
cfg_files=()
cfg_files+=/boot/octopi-cam2.txt
if [[ -d ${config_dir} ]]; then
  cfg_files+=( `ls ${config_dir}/*.txt` )
fi

cd /root/bin
sudo nano webcam3d
# Folgende Zeile anpassen
cfg_files=()
cfg_files+=/boot/octopi-cam3.txt
if [[ -d ${config_dir} ]]; then
  cfg_files+=( `ls ${config_dir}/*.txt` )
fi

```

```bash
cd /etc/systemd/system/

sudo cp webcamd.service webcamd2.service
sudo cp webcamd.service webcamd3.service

sudo nano /etc/systemd/system/webcamd2.service
# ändere webcam -->webcam2d
sudo systemctl enable webcamd2

sudo nano /etc/systemd/system/webcamd3.service
# ändere webcam -->webcam2d
sudo systemctl enable webcamd3
```

Download Plugin "Multicam"

```bash
http://192.168.2.21:8081/?action=stream
http://192.168.2.21:8082/?action=stream
```
