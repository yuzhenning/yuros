# P40 X99 Server AI station
## Part 1 Prepar for GPU

===
### Step1 Check pci hardware information

check nvidia hardware
```
lspci | grep -i nvidia
```
result:
```
03:00.0 VGA compatible controller: Advanced Micro Devices, Inc. [AMD/ATI] Cedar [Radeon HD 5000/6000/7350/8350 Series]
```

check vga display hardware
```
lspci | grep -i vga
```
result:
```
04:00.0 3D controller: NVIDIA Corporation GP102GL [Tesla P40] (rev a1)
```

Done!

===

### Step2 install yum tools
locate and edit source file:
```
cd /etc/apt
sudo gedit source.list
```

added follows command in the first line:
```
deb http://archive.ubuntu.com/ubuntu/ trusty main universe restricted multiverse
```

reload source:
```
sudo apt-get update
sudo apt-get install yum
```

screen display the following information that lake of dependence packages:
```
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Some packages could not be installed. This may mean that you have
requested an impossible situation or if you are using the unstable
distribution that some required packages have not yet been created
or been moved out of Incoming.
The following information may help to resolve the situation:

The following packages have unmet dependencies:
 yum : Depends: python-sqlitecachec but it is not going to be installed
       Depends: python-urlgrabber but it is not going to be installed
E: Unable to correct problems, you have held broken packages.
```


install depend package:
```
sudo apt-get install python-sqlitecachec
```
```
sudo apt-get install python-urlgrabber
```

reinstall yum tools
```
sudo apt-get install yum
```

Done!

===

### Step3 install P40 Nvidia Drivers

Check Suitable Nvidia Drivers 
```
ubuntu-drivers devices
```
display follows:
```
== /sys/devices/pci0000:00/0000:00:03.0/0000:04:00.0 ==
modalias : pci:v000010DEd00001B38sv000010DEsd000011D9bc03sc02i00
vendor   : NVIDIA Corporation
model    : GP102GL [Tesla P40]
driver   : nvidia-driver-535-server - distro non-free
driver   : nvidia-driver-535 - third-party non-free
driver   : nvidia-driver-470 - distro non-free
driver   : nvidia-driver-390 - distro non-free
driver   : nvidia-driver-418-server - distro non-free
driver   : nvidia-driver-450-server - distro non-free
driver   : nvidia-driver-470-server - distro non-free
driver   : nvidia-driver-525 - distro non-free
driver   : nvidia-driver-545 - third-party non-free recommended
driver   : nvidia-driver-525-server - distro non-free
driver   : xserver-xorg-video-nouveau - distro free builtin
```


**Added PPA sources list:**
```
sudo add-apt-repository ppa:graphics-drivers/ppa
```

Check and auto install ubuntu-nvidia drivers:
```
sudo ubuntu-drivers autoinstall
```

There are lack of depended as follows:
```
[sudo] password for yubuntust: 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Some packages could not be installed. This may mean that you have
requested an impossible situation or if you are using the unstable
distribution that some required packages have not yet been created
or been moved out of Incoming.
The following information may help to resolve the situation:

The following packages have unmet dependencies:
 nvidia-driver-535 : Depends: nvidia-utils-535 (= 535.129.03-0ubuntu0.20.04.1) but it is not going to be installed
                     Recommends: libnvidia-compute-535:i386 (= 535.129.03-0ubuntu0.20.04.1)
                     Recommends: libnvidia-decode-535:i386 (= 535.129.03-0ubuntu0.20.04.1)
                     Recommends: libnvidia-encode-535:i386 (= 535.129.03-0ubuntu0.20.04.1)
E: Unable to correct problems, you have held broken packages.
```

Install depended packages:
```
sudo apt-get install nvidia-utils-535
```

**tips**
error after apt-get update
```
E: Could not get lock /var/lib/apt/lists/lock. It is held by process 1554 (packagekitd)
N: Be aware that removing the lock file is not a solution and may break your system.
E: Unable to lock directory /var/lib/apt/lists/
```

Please delete relate files as follows:
```
sudo rm /var/lib/apt/lists/lock
```

**important**

** Personal P40-Driver **

install recommand driver:
```
sudo apt-get install nvidia-driver-470
```

if there are any mistakes or error needs uninstall:
```
sudo apt-get --purge remove nvidia*
sudo apt-get autoremove
```

Finish install deriver information:
```
nvidia-smi

Thu Jan  4 17:27:04 2024       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 470.223.02   Driver Version: 470.223.02   CUDA Version: 11.4     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  Tesla P40           Off  | 00000000:04:00.0 Off |                  Off |
| N/A   31C    P8    17W / 250W |      9MiB / 24451MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A      1250      G   /usr/lib/xorg/Xorg                  4MiB |
|    0   N/A  N/A      1846      G   /usr/lib/xorg/Xorg                  4MiB |
+-----------------------------------------------------------------------------+
```

Done!

===

