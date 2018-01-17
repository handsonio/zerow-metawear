# Zero W Metawear 

Zero-W-Metawear helps you to setup your Raspberry Pi Zero W to communicate with the Metawear smart sensor through a node.js application.


## The Raspbian Operating System

The following setup has been tested with **Raspian 8 Jessie Lite**, download the official image [here](http://downloads.raspberrypi.org/raspbian_lite/images/raspbian_lite-2017-04-10/)

## Burn the image and mount it

- Burn the Raspbian Image onto a SD card, use [Etcher.io](https://etcher.io/) to do it. Piece of cake !
- Mount the SD card on your computer

## Prepare the board to accept ssh connection through usb ethernet

Now we need to enable the Usb On-The-Go (OTG) mode which comes with different modules, here we need USB Ethernet module (g_ether) and make sure we use the `dwc2` USB driver (more info [here](https://gist.github.com/gbaman/50b6cca61dd1c3f88f41)) to be able to ssh our device.

- Edit `config.txt` and put at the very bottom 

```
dtoverlay=dwc2
```

- Edit `cmdline.txt` and insert right after `rootwait` 

```
modules-load=dwc2,g_ether
```

- Create an empty **ssh** file on the drive labeled **boot** to enable SSH on the Pi (disabled by default)

## Configure your wifi network

- Create a file called wpa_supplicant.conf and setup your WiFi network

Here is an example

```
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=BE

network={
	ssid="YourNetworkSsid"
	psk="yourPassword"
	id_str="Your primary network"
}

network={
	ssid="YourSecondNetworkSsid"
	psk="yourPassword"
	id_str="Your secondary network"
}
```

## Boot your little beast !

- Eject your SD Card
- Put the SD card back into the Pi Zero W
- Plug your USB cable into the port labelled **USB**
- Connect to pi@raspberrypi.local
- Default password is `raspberry`
- Install git `sudo apt-get install git`

## Install Node.js

```
cd ~
wget https://nodejs.org/dist/v4.8.2/node-v4.8.2-linux-armv6l.tar.gz
tar -xzf node-v4.8.2-linux-armv6l.tar.gz
node-v4.8.2-linux-armv6l/bin/node -v
sudo cp -R * /usr/local/
export PATH=$PATH:/usr/local/bin
node -v
npm -v

```

## Install Git !

```sudo apt-get update```
```sudo apt-get install git```

## Setup [node-metawear](https://www.npmjs.com/package/node-metawear) dependencies

- Installation of required dependencies `sudo apt-get install bluetooth bluez-utils libbluetooth-dev`
```
	Package bluez-utils is not available, but is referred to by another package.
	This may mean that the package is missing, has been obsoleted, or
	is only available from another source
	However the following packages replace it:
  	bluez
```
- Attention : use `bluez` instead


