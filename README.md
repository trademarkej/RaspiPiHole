# RASPI-Pi-Hole
Configuration files from my Raspi 3b Pi-Hole box

### Getting Started
These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites
  * This project is based on Raspbian Buster with Desktop (or higher) available here:  [https://www.raspberrypi.org/downloads/raspbian/](http://)

### Installing

1. Copy the **YYYY-MM-DD-raspbian-<build>.img** file to the micro sd card using Balena Etcher
2. Insert the newly imaged micro sd card into the Raspberry Pi and boot
3. (OPTIONAL) Once the image is fully expanded and Raspbian boots to the desktop, configure **eth0** to use a static IP
  * Right click on the network icon and select **Wireless & Wired Network Settings**
  * Select **Configure** -> **interface** -> **eth0**
  * Check
      * "Automatically configure empty options"
      * "Disable IPv6"
  * Enter the following values:
      * IPv4 Address:	192.168.1.250
      * Router:			192.168.1.254
      * DNS Servers:	8.8.8.8
      * DNS Search:		8.8.8.8
  * Reboot and verify w:
      * `ifconfig`

### Configuring Network Shares
1. Launch the Raspberry Pi Configuration utility from Start > Preferences or open a terminal window and enter the following command(s):
  * `sudo raspi-config`
      * System
          * Boot -> To CLI
          * Auto Login -> Login as user pi
          * Boot Options -> Wait for network at boot
          * Set Resolution
      * Interfaces
          * SSH -> Enabled
          * VNC -> Enabled

  * Reboot and verify w:
      * `df -h`

### Setting Up Remote Access
1. Install RealVNC & SSH
  * This should be done via the **raspi-config** **Start** > **Settings** > application
      * ~~sudo nano /boot/config.txt~~
      * ~~framebuffer_width=1920~~
      * ~~framebuffer_height=1024~~	

### Install / Configure Pi-hole
[https://www.myhelpfulguides.com/2018/07/15/install-pi-hole-raspbian-lite/](http://)
1. Open a terminal window and enter the following command(s):
  * `wget -O basic-install.sh https://install.pi-hole.net`
  * `sudo bash basic-install.sh`
  * Follow the prompts in the install gui selecting default options
      * Use Google for the upstream DNS
      * Make sure to record the Admin webpage login password

### Install / Configure Log2Ram
[https://goo.gl/Q3m3sq](http://)
1. Open a terminal window and enter the following command(s):
  * `curl -Lo log2ram.tar.gz https://github.com/azlux/log2ram/archive/master.tar.gz`
  * `tar xf log2ram.tar.gz`
  * `cd log2ram-master`
  * `chmod +x install.sh && sudo ./install.sh`
  * `cd ..`
  * `rm -r log2ram-master`
  * `sudo nano /etc/log2ram.conf`
      * Update the SIZE=###M value to SIZE=128M
  * Reboot and verify log2ram is mounted w:
      * `df -h`

### Install / Configure Fail2Ban
[https://goo.gl/Q3m3sq](http://)
1. Open a terminal window and enter the following command(s):
  * `curl -Lo log2ram.tar.gz https://github.com/azlux/log2ram/archive/master.tar.gz`
  * `tar xf log2ram.tar.gz`
  * `cd log2ram-master`
  * `chmod +x install.sh && sudo ./install.sh`
  * `cd ..`
  * `rm -r log2ram-master`
  * `sudo nano /etc/log2ram.conf`
      * Update the SIZE=###M value to SIZE=128M
  * Reboot and verify log2ram is mounted w:
      * `df -h`

### Testing:
On a seperate computer, login to the Pi-hole Admin webpage using the previously reported login password
1. [http://192.168.1.250/admin](http://)

### Securing DNS w Cloudflare:
Using the following guide, secure the DNS routing on the pi hole server using Cloudflare
1. [https://scotthelme.co.uk/securing-dns-across-all-of-my-devices-with-pihole-dns-over-https-1-1-1-1/](http://)

### Creating https certs using Let's Encrypt:
1. [https://scotthelme.co.uk/setting-up-le/](http://)

### Author:
trademarkej

### License
This project is licensed under the MIT License - see the LICENSE.md file for details

### Acknowledgments
N/A