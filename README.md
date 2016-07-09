# Crazyflie PC client (Ubuntu Linux)

Main Modification

    ZMQ input enabled and automated Thrust commands sent from PC to crazyflie

Usage

Assumptions 

1. Crazyflie USB PA Hardware 
2. CFlib installed ( follow https://github.com/bitcraze/crazyflie-lib-python )
3. The client will be run from source
4. Python 3 installed
5. Following dependencies satisfied
        * Python 3.4
        * PyUSB
        * libusb 1.X (works with 0.X as well)
        * PyQtGraph
        * ZMQ
        * PyQt4
    For Ubuntu (15.04) run:
    sudo apt-get install python3 python3-pip python3-pyqt4 python3-zmq python3-pyqtgraph
    sudo pip3 install pyusb==1.0.0b2


### STEPS

 Launching the GUI application

1. To launch the GUI application in the source folder, got to bin folder and type:

   python3 cfclient

2. Gui should open and scan for the crazyflie and connect.
   (verify that chnage in crazyflie position is reflected in client Flightdata)

3. Input device type is set to zmq@tcp://127.0.0.1/1212

4. Open another terminal. Go to examples folder and run 

   python3 zmqclientinput.py

5. Crazyflie starts lifting (motors spins). client screen would show the target thrust and actual thrust.


For more info see [wiki](http://wiki.bitcraze.se/ "Bitcraze Wiki") 
https://github.com/bitcraze/crazyflie-clients-python
https://wiki.bitcraze.io/doc:crazyflie:client:pycfclient:zmq#input_device

The Crazyflie PC client enables flashing and controlling the Crazyflie.
There's also a Python library that can be integrated into other applications
where you would like to use the Crazyflie.


Extra (for Radio HW setup)
---------------------------

### Setting udev permissions

The following steps make it possible to use the USB Radio without being root.

Note: If using a fresh Debian install, you may need to install sudo first
(executing exit command to exit from root shell first):

```
su -
apt-get install sudo
```

Now, with sudo installed, you should be able to do the following commands

```
sudo groupadd plugdev
sudo usermod -a -G plugdev <username>
```

Create a file named ```/etc/udev/rules.d/99-crazyradio.rules``` and add the
following:
```
SUBSYSTEM=="usb", ATTRS{idVendor}=="1915", ATTRS{idProduct}=="7777", MODE="0664", GROUP="plugdev"
```

To connect Crazyflie 2.0 via usb, create a file name ```/etc/udev/rules.d/99-crazyflie.rules``` and add the following:
```
SUBSYSTEM=="usb", ATTRS{idVendor}=="0483", ATTRS{idProduct}=="5740", MODE="0664", GROUP="plugdev"
```

Restart the computer and you are now able to access the USB radio dongle
without being root.
