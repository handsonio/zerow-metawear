# Zero W Metawear 

Zero-W-Metawear helps you to setup your Raspberry Pi Zero W to communicate with the Metawear smart sensor through a node.js application.

## The Raspbian Operating System


- Burn the Raspbian Image onto a SD card, DO NOT USE THE NOOB distribution
- Mount the SD card on your computer

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
- Create a file called wpa_supplicant.conf and setup your WiFi network

```
network={
	ssid="YourNetworkSsid"
	psk="yourPassword"
}
```

- Eject your SD Card
- Put the SD card back into the Pi Zero W
- Plug your USB cable into the port labelled **USB**
- Connect to pi@raspberrypi.local
- Default password is `raspberry`
- Install git `sudo apt-get install git`

- Install Node.JS 

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


