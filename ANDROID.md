## Context ADB commands

Create /etc/profile.d/adb.sh
```
export ANDROID_HOME=/home/max/Android/Sdk/
export PATH=$PATH:$ANDROID_HOME/platform-tools
```

## Connect device without elevated privileges

Identify the vendor and product ID for your device
```
# lsusb
...
Bus 001 Device 007: ID 18d1:4ee2 Google Inc. Nexus Device (debug)
...
```
Create /etc/udev/rules.d/99-adb.rules
```
 SUBSYSTEM=="usb", ATTR{idVendor}=="18d1", ATTR{idProduct}=="4ee2", MODE="0666"
```
Reload udev rules
```
# udevadm control --reload-rules
```
Unplug and plug the device
```
$ adb devices
```