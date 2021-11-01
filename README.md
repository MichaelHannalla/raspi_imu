
# raspi_imu
A repository for interfacing IMU sensors using I2C communication on a Raspberry Pi 4.

## Preparing the Raspberry Pi
Go through the next steps to enable the I2C communication module on the pi and install required dependencies. 

### Enabling I2C Module
On the Pi, I2C is disabled by default. The first thing to do, is run the command `sudo nano /etc/modprobe.d/raspi-blacklist.conf` . In this file, there is a comment, and two lines. Add a hash before the I2C line, to comment out the blacklisting of it. \
Your file should look like this:

	# blacklist spi and i2c by default (many users don't need them)  
	  
	blacklist spi-bcm2708  
	#blacklist i2c-bcm2708

**[NOTE]: If you find the file is blank, skip this step!**

### Enabling Kernel I2C Module
The next thing to do is add the I2C module to the kernel. Run the command `sudo nano /etc/modules` . \
Your file should look like this:
  
	# /etc/modules: kernel modules to load at boot time.  
	#  
	# This file contains the names of kernel modules that should be loaded  
	# at boot time, one per line. Lines beginning with "#" are ignored.  
	# Parameters can be specified after the module name.  
	  
	snd-bcm2835  
	i2c-dev

### Installing Dependency Packages
1. Run `sudo apt update`
2. Then `sudo apt install i2c-tools`
3. Then `sudo apt-get install python-smbus`
4. Add the Pi user to the I2C access group, by running the command `sudo adduser pi i2c`
5. Reboot using `sudo reboot`

### Enabling the I2C Peripheral 
1. Enter `sudo raspi-config`
2. Go to `Interface Settings`
3. Enable the I2C Module 

### Testing the Module 
Run the command `i2cdetect -y 1` to see if the i2c works.
