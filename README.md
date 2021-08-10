# ubuntu-server-config

> This reposiroty provides some overview about installing and configuring Ubuntu 20.04 Server Edition

> ps. I am installing it on my old ASUS laptop. 

*Thanks to Dejan Tucakob* : see his guide here ---> [Reference](https://phoenixnap.com/kb/install-ubuntu-20-04)

------------------------------------------------------

##  Step 1: Download the Installation Media 

1. In your brownser, visit [Ubuntu Server](https://ubuntu.com/download/server) and download Ubuntu Server 20.04.02 LTS server 
2. Click on the green Download button. You will be taken to a thank-you page.
3. Save the file to a location of your choise.

## Step 2: Create Bootable USB Drive on Windows

> You will need a USB drive with 4GB or more. This process will delete all data on the USB drive. Make sure to backup any existing data on the USB drive.

> You’ll need to install a third-party utility called Rufus to create a USB bootable drive.

1. [Download the Rufus utility](https://rufus.ie/en/). Scroll down to the download section and click the link to download the latest version of Rufus.
2. Run the file once downloaded.
3. A pop-up dialog opens. You will be prompted whether you want to check for online updates. Select No.
4. The Rufus utility launches. Plug in the USB drive – you should see the drive pop up in the device field.
    
    + Set the USB as the device you wish to write to.
    + In the Boot Selection drop-down, click Disk or ISO Image.
    + Click the Select button to the right.
    + Browse and select the .iso Ubuntu file you downloaded earlier.

5. Click Start.

## Step 3:  Boot up Ubuntu from USB

1. Turn off your system. Make sure you remove all other USB devices, such as printers, memory cards, etc.
2. Insert the Ubuntu USB drive into the system and turn on your machine.

* There are two possible scenarios:

    + The computer boots the USB drive automatically.
    + You need to manually configure USB booting in the Boot Menu or BIOS/UEFI.

3.  To manually configure the boot order, tap the boot menu key about once or twice per second as soon as the computer powers on.

* The boot menu key may be different depending on your computer manufacturer. Below is a list of common boot keys associated to a brand:

    | BRAND     |   KEY             |
    | :-------- | :---------------: | 
    |Asus       |	F8 or Esc       |
    |Acer       |	F12, F9 or Esc  |
    |Compaq     |	F9 or Esc       |
    |Dell       |	F12             |
    |eMachines  |	F12             |
    |Fujitsu    |	F12             |
    |HP         |	F9 or Esc       |
    |Lenovo     |	F8, F10 or F12  |
    |Samsung    |	F2, F12 or Esc  |
    |Toshiba    |	F1              |

4. Once you see your boot menu, use the arrows to pick the Ubuntu media to boot from. For a DVD, the entry will usually have DVD or Optical in the name. USB is usually labeled USB. Then, Your system should start loading the Ubuntu live disc menu.

## Step 4: Booting the USB installer

* [See here for detailed information](https://ubuntu.com/server/docs/install/step-by-step)

1. See below a summary of tasks:
    
    + Choose your language
    + Update the installer (if offered)
    + Select your keyboard layout
    + Do not configure networking (the installer attempts to configure wired network interfaces via DHCP, but you can continue without networking if this fails)
    + Do not configure a proxy or custom mirror unless you have to in your network
    + For storage, leave “use an entire disk” checked, and choose a disk to install to, then select “Done” on the configuration screen and confirm the install
    + Enter a username, hostname and password
    + Just select Done on the SSH and snap screens
    + You will now see log messages as the install is completed
    + Select restart when this is complete, and log in using the username and password provided




