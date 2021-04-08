# Raspberry Pi

## Initial setup (headless)

1. On the sd card in `/` do the following

```bash
touch ssh
vi wpa_supplicant.conf
```

```bash
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=<Insert 2 letter ISO 3166-1 country code here>

network={
 ssid="<Name of your wireless LAN>"
 psk="<Password for your wireless LAN>"
}
```

## Rotate the lcd display

```bash
sudo vi /boot/config.txt
lcd_rotate=2
...
sudo reboot
```

## Update the Raspberry Pi

```bash
sudo apt update
sudo apt dist-upgrade
```

## Install `python3` (including `Tkinter`)

```bash
sudo apt install python3-pip
sudo apt install python3-tk
```

## Configure python alternative

```bash
sudo update-alternatives --install /usr/bin/python python $(which python) 1
sudo update-alternatives --install /usr/bin/python python $(which python3) 2

sudo update-alternatives --list python
sudo update-alternatives --config python

python --version
```

## Configure a splash screen

1. If you are using Raspery Pi OS Lite you need to install [plymouth](https://github.com/HerbFargus/Raspberry-Pi-Scripts/wiki/Plymouth)

    ```bash
    sudo apt install plymouth plymouth-themes -y
    sudo apt install pix-plym-splash -y
    ```

2. Follow the instruction at https://scribles.net/customizing-boot-up-screen-on-raspberry-pi/

3. In addition to these instruction you need to comment out the following line in `/boot/config.txt`

    ```bash
    # dtoverlay=vc4-fkms-v3d
    ```