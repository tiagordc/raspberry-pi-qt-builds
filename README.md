# rpi-build-qt-pyqt

Build the latest Qt5 and PyQt5 on a Raspberry Pi (no cross compiling)

Tested with Qt5.15.2 and PyQt5-5.15.2 on a Raspberry Pi 4 Model B 4GB

Also tested to work with PyInstaller and PyArmor to create standalone packages

Could only make it work with sip 4.19, recent versions break the compatibility with PyInstaller

# Build

1. Uncomment source line in sources-list

    * sudo nano /etc/apt/sources.list
    
      ![sources](images/sources.png)
    
    * ctrl+x and y

2. Update your system

    * sudo apt update
    * sudo apt full-upgrade
    * sudo reboot now
    
3. Install [dependencies](https://wiki.qt.io/Building_Qt_5_from_Git) - not sure if all these are really required

	  * sudo apt-get build-dep qt5-default
	  * sudo apt-get install '^libxcb.*-dev' libx11-xcb-dev libglu1-mesa-dev libxrender-dev libxi-dev libxkbcommon-dev libxkbcommon-x11-dev
	  * sudo apt-get install flex bison gperf libicu-dev libxslt-dev ruby nodejs
	  * sudo apt-get install libxcursor-dev libxcomposite-dev libxdamage-dev libxrandr-dev libxtst-dev libxss-dev libdbus-1-dev libevent-dev libfontconfig1-dev libcap-dev libpulse-dev libudev-dev libpci-dev libnss3-dev libasound2-dev libegl1-mesa-dev
	  * sudo apt-get install libasound2-dev libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev libgstreamer-plugins-bad1.0-dev
	  * sudo apt-get install freeglut3-dev
	  * sudo apt install libclang-6.0-dev llvm-6.0
  
4. Run the Qt build script

    * wget https://raw.githubusercontent.com/tiagordc/raspberry-pi-qt-builds/master/build-qt.sh
    * sudo chmod +x build-qt.sh
    * sh build-qt.sh

5. Qt is now build on /home/pi/qtbuild. Install it to proceed with PyQt

    * cd /
    * sudo tar xf /home/pi/qtbuild/**Qt5.15.2-rpi-bin-minimal.tgz**

6. Add Qt to PATH

    * nano ~/.bashrc
        * export LD_LIBRARY_PATH=/usr/local/**Qt-5.15.2**/lib:$LD_LIBRARY_PATH
        * export PATH=/usr/local/**Qt-5.15.2**/bin:$PATH
      
    	![path](images/path.png)

7. Build PyQt5

    * sudo apt-get install sip-dev
    * cd /usr/src
    * sudo wget https://www.riverbankcomputing.com/static/Downloads/sip/4.19.24/sip-4.19.24.tar.gz
    * sudo wget https://files.pythonhosted.org/packages/28/6c/640e3f5c734c296a7193079a86842a789edb7988dca39eab44579088a1d1/PyQt5-5.15.2.tar.gz
    * sudo tar xzf sip-4.19.24.tar.gz
    * sudo tar xzf PyQt5-5.15.2.tar.gz

    * cd sip-4.19.24
    * sudo python3 configure.py --sip-module PyQt5.sip
    * sudo make -j4
    * sudo make install

    * cd ../PyQt5-5.15.2
    * sudo python3 configure.py --qmake /usr/local/Qt-5.15.2/bin/qmake --confirm-license
    * sudo make -j4
    * sudo make install

8. Test

    * cd
    * sip -V
    * sudo wget https://raw.githubusercontent.com/tiagordc/rpi-build-qt-pyqt/master/test.py
    * python3 test.py

# References

1. https://wiki.qt.io/Native_Build_of_Qt5_on_a_Raspberry_Pi
2. https://wiki.qt.io/Native_Build_of_Qt_5.4.1_on_a_Raspberry_Pi
3. https://wiki.qt.io/Building_Qt_5_from_Git
4. https://doc.bccnsoft.com/docs/PyQt5/installation.html
