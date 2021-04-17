- [Introduction](#introduction)
- [Tings To Do Post Linux Install](#tings-to-do-post-linux-install)
  - [System Update/Upgrade](#system-updateupgrade)
  - [Customizations](#customizations)
    - [Gnome Tweak Tool](#gnome-tweak-tool)
    - [OCS-Install (For gnome themes)](#ocs-install-for-gnome-themes)
    - [Fusuma (multi-touch gestures)](#fusuma-multi-touch-gestures)
  - [Dev Tools](#dev-tools)
    - [Sublime](#sublime)
    - [VIM](#vim)
    - [VS Code](#vs-code)
    - [LAMP Stack](#lamp-stack)
      - [Maria DB](#maria-db)
      - [Apache](#apache)
      - [PHP](#php)
      - [PHPMYADMIN](#phpmyadmin)
    - [Node.js](#nodejs)
    - [Composer](#composer)
    - [Postman](#postman)
      - [As a Snap](#as-a-snap)
      - [Or Via Flatpak](#or-via-flatpak)
  - [Browsers](#browsers)
    - [firefox](#firefox)
    - [Brave Browser](#brave-browser)
    - [Google Chrome](#google-chrome)
  - [Game Drivers](#game-drivers)
    - [Steam](#steam)
    - [Lutris](#lutris)
    - [Vulkan](#vulkan)
  - [Other Packages and Applications](#other-packages-and-applications)
    - [Spotify](#spotify)
    - [VLC Media Player](#vlc-media-player)
    - [QBittorrent](#qbittorrent)
    - [GIMP](#gimp)
    - [Krita](#krita)
    - [Inkscape](#inkscape)
    - [Telegram](#telegram)
    - [Snap](#snap)
    - [Flatpak](#flatpak)
    - [Simplenote](#simplenote)

# Introduction

List of command and things to do after a fresh install of debian/ubuntu based linux. These configurations and packages are based on my requirements.

# Tings To Do Post Linux Install

## System Update/Upgrade

___

    sudo apt update -y

    sudo apt upgrade -y

<br />

## Customizations

___

### Gnome Tweak Tool

    sudo apt install gnome-tweak-tool

<br />

### OCS-Install (For gnome themes)

    sudo apt install libqt5svg5 qml-module-qtquick-controls

    sudo dpkg -i /path/to/ocs-url*.deb

Source: <https://www.pling.com/p/1136805/>

<br />

### Fusuma (multi-touch gestures)

Add current user to the input group.

    sudo gpasswd -a $USER input
Then log out and log back in (This is important). Then,

    sudo apt install libinput-tools

    sudo apt install xdotool

If Ruby isn't installed :

    sudo apt install ruby

Now install fusuma

    sudo gem install fusuma

Go to your config folder in home directory.

    cd ~/.config
Now create a folder named fusuma

    mkdir fusuma

    cd fusuma
In there create a file called config.yml

    touch config.yml
Now you can use your favourite text editor to enter the contents in this file.

    nano config.yml

and paste the contents of [config.yml](config.yml)

sources:

- <https://github.com/iberianpig/fusuma/blob/master/README.md>

- <https://askubuntu.com/questions/1034624/touchpad-gestures-in-ubuntu-18-04-lts>

<br />

## Dev Tools

___

### Sublime

    wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -

    echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list

    sudo apt update -y

    sudo apt install sublime-text

source: <https://www.ubuntuupdates.org/ppa/sublime>

<br />

### VIM

    sudo apt install vim

<br />

### VS Code

    curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg

    sudo install -o root -g root -m 644 microsoft.gpg /etc/apt/trusted.gpg.d/- [Introduction](#introduction)

    sudo sh -c 'echo "deb [arch=amd64] <https://packages.microsoft.com/repos/vscode> stable main" > /etc/apt/sources.list.d/vscode.list'

    sudo apt install apt-transport-https

    sudo apt update -y

    sudo apt install code

source: <https://www.ubuntuupdates.org/ppa/vscode>

<br />

### LAMP Stack

#### Maria DB

    sudo apt install software-properties-common mariadb-server mariadb-client

    sudo mysql_secure_installation 

Creating new user

    CREATE USER 'ritesh'@'localhost' IDENTIFIED BY 'password';

    GRANT ALL PRIVILEGES ON * . * TO 'ritesh'@'localhost';

    FLUSH PRIVILEGES;

<br />

#### Apache

    sudo apt install -y apache2 apache2-utils
    
    sudo systemctl reload apache2

    sudo systemctl enable apache2

    sudo systemctl is-enabled apache2

<br />

#### PHP

    sudo apt install php libapache2-mod-php php-cli php-fpm php-json php-pdo php-mysql php-zip php-gd  php-mbstring php-curl php-xml php-pear php-bcmath

    sudo a2enmod php7.4

    echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/phpinfo.php

<br />

#### PHPMYADMIN

    sudo add-apt-repository ppa:phpmyadmin/ppa

    sudo apt update

    sudo apt install phpmyadmin

    sudo nano /etc/apache2/conf-enabled/phpmyadmin.conf

and paste the content of the [phpmyadmin.conf](phpmyadmin.conf)

    sudo systemctl restart apache2

sources:

- <https://github.com/phpmyadmin/phpmyadmin/issues/15515#issuecomment-548521407>

- <https://websiteforstudents.com/install-phpmyadmin-latest-version-on-ubuntu-16-04-18-04-with-apache2-mariadb-and-php-7-2/>

- <https://computingforgeeks.com/how-to-install-lamp-stack-on-ubuntu/>

<br />

### Node.js

    sudo apt install nodejs

    sudo apt install npm

however some of the linux distro installs old version of node. To install the latest version:

    sudo apt install curl

    curl -fsSL https://deb.nodesource.com/setup_15.x | sudo -E bash -

    sudo apt install nodejs

sources:

- <https://www.how2shout.com/how-to/how-to-install-node-js-on-ubuntu-19-04.html>
- <https://github.com/nodesource/distributions>

<br />

### Composer

    sudo apt install composer

<br />

### Postman

#### As a Snap

Install [Snap](#snap) if not installed

    sudo apt install snapd

    sudo apt install postman

#### Or Via Flatpak

Install [Flatpak](#flatpak) if not installed

    sudo apt install flatpak

    sudo flatpak install flathub com.gettpostman.Postman

<br />

## Browsers

___

### firefox

is pre-installed with almost all linux

<br />

### Brave Browser

    sudo apt install apt-transport-https curl

    curl -s <https://brave-browser-apt-release.s3.brave.com/brave-core.asc> | sudo apt-key --keyring /etc/apt/trusted.gpg.d/brave-browser-release.gpg add -

    echo "deb [arch=amd64] <https://brave-browser-apt-release.s3.brave.com/> stable main" | sudo tee /etc/apt/sources.list.d/brave-browser-release.list

    sudo apt update

    sudo apt install brave-browser

source: <https://brave-browser.readthedocs.io/en/latest/installing-brave.html#linux>

<br />

### Google Chrome

    wget <https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb>

    sudo dpkg -i google-chrome-stable_current_amd64.deb

<br />

## Game Drivers

___

### Steam

Usually steam or steam installer is available on the software store provided of a distro. If steam is not available from the store:

    sudo add-apt-repository multiverse

    sudo apt update

    sudo apt install steam

source: <https://www.wikihow.com/Install-Steam-on-Linux>

<br />

### Lutris

    sudo apt install wine winetricks

    sudo apt install lutris

<br />

### Vulkan

    sudo apt install libvulkan1 mesa-vulkan-drivers vulkan-utils

source: <https://linuxconfig.org/install-and-test-vulkan-on-linux>

<br />

## Other Packages and Applications

### Spotify

    sudo apt install spotify

<br />

### VLC Media Player

    sudo apt install ubuntu-restricted-extras

    sudo apt install vlc

<br />

### QBittorrent

    sudo apt install qbittorrent

<br />

### GIMP

    sudo apt install gimp

<br />

### Krita

    sudo apt install krita

<br />

### Inkscape

    sudo apt install inkscape

<br />

### Telegram

    sudo apt install telegram-desktop

<br />

### Snap

    sudo apt install snapd

<br />

### Flatpak

    sudo add-apt-repository ppa:alexlarsson/flatpak
    
    sudo apt update 
    
    sudo apt install flatpak

    sudo apt install gnome-software-plugin-flatpak

    flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo

<br />

### Simplenote

    wget https://github.com/Automattic/simplenote-electron/releases/download/v1.16.0/Simplenote-linux-1.16.0-amd64.deb

    sudo dpkg -i Simplenote-linux-.....deb

<br />
