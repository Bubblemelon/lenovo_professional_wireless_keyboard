# Linux driver for Lenovo Professional Wireless Keyboard Combo

## Installation    

```bash
git clone https://github.com/Bubblemelon/lenovo_professional_wireless_keyboard.git

cd ~/lenovo_professional_wireless_keyboard

./install.sh

rm -rf ~/lenovo_professional_wireless_keyboard
```
## Repo Details  

`./install.sh` creates a systemd service that enables and runs lenovo_keyboard.service in the background. Thus your levono keyboard will not work before PID(1).


The keybindings in `kbdusb.c` is not linked with ASCII in the `mapkey()` function,


### Main Difference from Forked Origin  

This case does not work with my keyboard:
```
case 0x32:
  keysent = KEY_BACKSLASH;
  break;
```
Meaning, the <kdb> \ </kdb> and <kdb> | </kdb> keys (the key above <kdb>Enter</kdb>) does not work. I am unsure of the reason.

So I simply replaced the <kdb>-</kdb> key on the **Keypad** section of my Lenovo Keyboard with the following:

```bash
// changing this to \ (backslash) and | (pipe) on keypad: ( was previously KEY_KPMINUS )
case 0x56:
keysent = KEY_BACKSLASH;
break;
```


### Should work on:  

Ubuntu: 16.04  
Kernel: 4.10  

My Machine Info:

```bash
cat /etc/os-release

NAME=Fedora
VERSION="28 (Workstation Edition)"
ID=fedora
VERSION_ID=28
PLATFORM_ID="platform:f28"
PRETTY_NAME="Fedora 28 (Workstation Edition)"
ANSI_COLOR="0;34"
CPE_NAME="cpe:/o:fedoraproject:fedora:28"

uname -r

kernel-4.16.9-300.fc28.x86_64
```
