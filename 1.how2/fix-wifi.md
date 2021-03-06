# Ubuntu SERVER 20.04  - Fixing the WIFI 

* The  Ubuntu 20.04 server installation software does not include wireless network support packages, so it relies on the user to enable the Wi-Fi connection.

* I didn't have ethernet connection either. 

------------------------------------------------------

##  Step 1: Download WPA Supplicant Package and Its Dependecies 

* Since the server has no wired ethernet connection, you need to download the WPA supplicant package (wpasupplicant) and two of its dependencies (libnl-route-3–200, libpcsclite1) on another machine with an internet connection, then transfer them to the server using a flash/external drive.



| File Name         |  Link       | What is it? |
| :-------------:   | :---------: | :---------: |
| wpasupplicant     | [Link-1](http://mirrors.kernel.org/ubuntu/pool/main/w/wpa/wpasupplicant_2.9-1ubuntu4_amd64.deb)      | client support for WPA and WPA2 (IEEE 802.11i)            |
| libnl-route-3–200 | [Link-2](http://mirrors.kernel.org/ubuntu/pool/main/libn/libnl3/libnl-route-3-200_3.4.0-1_amd64.deb) |library for dealing with netlink sockets — route interface |
| libpcsclite1      | [Link-3](http://mirrors.kernel.org/ubuntu/pool/main/p/pcsc-lite/libpcsclite1_1.8.26-3_amd64.deb)     |library for dealing with netlink sockets — route interface |


## Step 2: Transfer and Install files from flash/external drive to Ubuntu Server

* On your UBUNTU server terminal, do the following.

1. Navigate to /media.

    ```bash
    cd /media 
    ```

2. Create a folder called usb.
    
    ```bash
    mkdir usb
    ```

3. Find a device name for the flash/external/USB drive after you plug it into the server:

    ```bash
    sudo fdisk -l        # A USB flash disk is usally list at: `/dev/sdv1/`
    ```

4. Mount the flash/external/usb drive:

    ```bash
    sudo mount  /dev/sdb1 ./usb
    ```

5. Install WPA supplicant package and its dependecies:

    ```bash
    sudo dpkg -u *.deb       # Make sure you are in the correct folder with the 3 files.
    ```

## Step 3: Find Wireless Interface Name 

* The Linux kernel lists network interface names via symlinks in /sys/class/net, whereas the wireless network interfaces are named wlp2s0, wlp3s0, and so on:

1. On your Ubuntu server terminal, type:

    ```bash
    ls /sys/class/net | grep -i wlp
    ```

## Step 4: Create a NetPlan Configuration File

* To configure netplan, make a copy of the existing configuration file, then create a new one under /etc/netplan/ with a .yaml extension:

* On your ubuntu server terminal, do the following:

1. Create a backup of the original file.

    ```bash
    sudo cp /etc/netplan/00-installer-config.yaml /etc/netplan/00.bakup
    ```

2. Create a new configuration file

    ```bash
    sudo vi /etc/netplan/00-installer-config.yaml
    ```

3. Edit the *.YAML* 

    ```bash

    network:
      ethernetes: {}
      wifis:
        wlp2s0:
          dhcp4: true
          optional:true
          access-points:
            "network_ssid_name":
              password: "**********"
      version: 2
      renderer: networkd
    ```

4. After saving the file, check you gateway default number, do the following:
    
    ```bash
    ip route
    ```
>   You can also do the following `ip a` and look for `wlp2s0` inet values.
>
>   The result will ve something like:
>
>       default via 192.168.1.1 dev wlp2s0 proto dhcp src 192.168.10.22 metric 600
>

5. Open `00-installer-config.yaml`.

    ```bash
    sudo vi /etc/netplan/00-installer-config.yaml
    ```

6. Edit the file with the information from `ip route` command.

    ```bash

    network:
      ethernetes: {}
      wifis:
        wlp2s0:
          dhcp4: no
          dhcp6: no
          optional:true
          addresses: [192.168.1.22/24]
          gateway4: 192.168.1.1
          nameservers:
            addresses: [1.1.1.1, 8.8.8.8]
          access-points:
            "network_ssid_name":
              password: "**********"
      version: 2
      renderer: networkd    

    ```
## Step 5: Apply the new Netplan Configuration
    
1. Generate backend and apply the new configuration.

    ```bash

    sudo netplan --debug generate
    sudo netplan appy

    ```

2. Now reboot the server:

    ```bash
    sudo reboot

    ```
3. Once reboot is done, check if you can access your internet:

    ```bash
    ping google.com
    ```

>   You should be abble to see:
>
>   PING google.com (142.250.217.142) 56(84) bytes of data.
>
>   64 bytes from lax31s19-in-f14.1e100.net (142.250.217.142): icmp_seq=1 ttl=65 time=139 ms

------------------------------------------------------
## [References](https://github.com/fcarvalhopacheco/ubuntu-server-config/blob/main/CREDITS.md#step-2)
