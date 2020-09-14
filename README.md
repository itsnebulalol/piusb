
# piUSB

Turn your \$10 Raspberry Pi Zero into a web USB stick!

---

## Prerequisites

-   Windows, Mac, or Linux computer
-   Internet connection
-   Raspberry Pi Zero (Wifi model not needed, but highly recommended)
-   16gb+ micro SD card (We always recommend Samsung SD cards)
-   SSH client (Older versions of Windows only)
-   **[OPTIONAL]** VNC Viewer

## Installation

#### SD Card Setup

1. Flash a 16gb+ micro SD card with Raspberry Pi OS Lite (if you'd like a graphical UI for VNC, you can use a regular version) using Etcher
2. Add a blank file called `ssh` to the root of the SD card (just `ssh`, nothing else)
3. Open the `cmdline.txt` file, and add `modules-load=dwc2,g_ether` to the end of the file (not on a new line)
4. Open the `config.txt` file, and add `dtoverlay=dwc2` to a new line on the end of the file

#### Web Software Setup

1. Plug in the Raspberry Pi
2. Wait 30-90seconds for the Pi to boot up
3. Open your SSH client (or terminal), and SSH into `pi@raspberrypi.local` (the default password is `raspberry`)
4. Type in `sudo raspi-config`, and "Expand Filesystem", now, if you'd like, you may change the hostname to something else, rather than "raspberry", for example, mine is "usb"
5. Restart when prompted
6. After you restart, copy and paste the following command:
   `sudo apt update && sudo apt install apache2 libapache2-mod-php mariadb-server mariadb-client php-bz2 php-mysql php-curl php-gd php-imagick php-intl php-mbstring php-xml php-zip zip unzip -y && sudo a2enmod rewrite`
7. During that command, MariaDB will prompt you to select a password, type in any password (but remember it)
8. Type `cd /var/www` (if you get an error, type `sudo mkdir /var/www && cd /var/www`)
9. To give access to the system, type `chmod 744 .` (DON'T MISS THE DOT AT THE END)
10. Type in `sudo git clone https://github.com/itsnebulalol/piusb.git`
11. Type `sudo mv piusb/. .` (AGAIN, DON'T MISS THE DOTS AT THE END)
12. Now, you can put in `sudo rm -rf piusb`
13. Navagate your browser to `http://raspberrypi.local/index.html` (or a different hostname if you changed it before)
14. And boom! Now you have your piUSB setup! To install Owncloud, keep reading on.

#### Owncloud Setup

1. To setup Owncloud, type `sudo mysql -u root -p`, then type in the password you created before.
2. Type `create database owncloud;` into the MariaDB prompt
3. Then, type `create user 'owncloud'@'localhost' identified by 'owncloud';` into the prompt
4. After that, type `grant all privileges on owncloud.* to 'owncloud'@'localhost';` into the prompt
5. Lastly, type `exit;` into the MariaDB prompt
6. Type `cd /var/www`
7. Now, you can type `sudo wget https://download.owncloud.org/community/owncloud-complete-20200731.zip` to start downloading Owncloud
8. To unzip Owncloud, type in `sudo unzip owncloud-complete-20200731.zip`
9. Now navigate your browser to `http://raspberrypi.local` (or a different hostname if you changed it before)
10. Select "Owncloud"
11. Type in a username and password, and make sure "Storage & database" is dropped down
12. Scroll down a little bit until you see the database information
13. Make sure MySQL/MariaDB is selected (if you don't see this, just ignore it)
14. The username is `owncloud`, the password is `owncloud`, the database name is `owncloud`, and the address is `localhost`
15. Click "Finish setup"
16. Login with the details you made in step 11.
17. Done! You have set up Owncloud!

<h3 align="center">If you have any problems, you can leave a GitHub issue.</h3>
<p align="center">Create a GitHub issue with the "Problem" template.</p>
