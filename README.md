# rpi-build-qt-pyqt

Build Qt5 and PyQt5 on a Raspberry Pi

Tested with Qt5.15.1 and PyQt5-5.15.2 on a Raspberry Pi 4 Model B 4GB

# Build

1. Uncomment source line in sources-list

    * sudo nano /etc/apt/sources.list
    
      ![sources](images/sources.png)
    
    * ctrl+x and y

2. Update your system

    * sudo apt update
    * sudo apt full-upgrade
    * sudo reboot now
    * sudo rpi-update
    * sudo reboot now
    
3. Install [dependencies](https://wiki.qt.io/Building_Qt_5_from_Git)

	  * sudo apt-get build-dep qt5-default
	  * sudo apt-get install build-essential perl python git
	  * sudo apt-get install '^libxcb.*-dev' libx11-xcb-dev libglu1-mesa-dev libxrender-dev libxi-dev libxkbcommon-dev libxkbcommon-x11-dev
	  * sudo apt-get install flex bison gperf libicu-dev libxslt-dev ruby
	  * sudo apt-get install libxcursor-dev libxcomposite-dev libxdamage-dev libxrandr-dev libxtst-dev libxss-dev libdbus-1-dev libevent-dev libfontconfig1-dev libcap-dev libpulse-dev libudev-dev libpci-dev libnss3-dev libasound2-dev libegl1-mesa-dev gperf bison nodejs
	  * sudo apt-get install libasound2-dev libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev libgstreamer-plugins-bad1.0-dev
	  * sudo apt install libclang-6.0-dev llvm-6.0
  
4. Download the Qt build script and check for the right version

    * wget https://raw.githubusercontent.com/tiagordc/raspberry-pi-qt-builds/master/build-qt.sh
    * sudo chmod +x build-qt.sh

5. Make sure the Pi boot into CLI and not desktop

    * sudo raspi-config

# Install

# References

1. https://wiki.qt.io/Native_Build_of_Qt5_on_a_Raspberry_Pi
2. https://wiki.qt.io/Native_Build_of_Qt_5.4.1_on_a_Raspberry_Pi
3. https://wiki.qt.io/Building_Qt_5_from_Git
4. https://doc.bccnsoft.com/docs/PyQt5/installation.html
