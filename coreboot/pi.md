# Installation Instructions for coreboot on X220 with RasPi3

## Prepare RasPi3
- get newest Raspberry Pi OS (I used the 64bit Version with recommended software) [https://www.raspberrypi.com/software/operating-systems/]
- copy iso on SD card
  <details>
    <summary>Get SD card info</summary>
    
    ```bash
    lsblk
    ```
  </details>
  <details>
    <summary>Copy on SD card using dd</summary>
    
    ```bash
    sudo dd if=/path/to/iso of=/path/to/sd bs=4M status=progress && sync
    ```
  </details>
- prepare **user**, **wifi** and **ssh** before first boot: All files have to be stored in boot partition! 
  <details>
    <summary>Create User</summary>
    
    ```bash
    echo "myuser:$(echo 'mypassword' | openssl passwd -6 -stdin)" > userconf
    ```
  </details>
  <details>
  <summary>Enable SSH</summary>
  
    ```bash
  touch ssh
    ```
  </details> 
  <details>
  <summary>Wifi configuration</summary>
  Create file named wpa_supplicant.conf
  
  ```bash
  country=DE
  ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
  update_config=1
  network={
     ssid="Your network name/SSID"
     psk="Your WPA security key"
     key_mgmt=WPA-PSK
  }
  ```
  </details>
- enable SPI Interface option
  <details>
  <summary>Enable SPI Interface</summary>
    
  ```bash
   sudo raspi-config
   # Choose [5] Interfacing options
   # P4 SPI -> Enable
   # Reboot Pi
   reboot
  ```
  </details>
- Update Rasperry Pi
  <details>
  <summary>Update Raspberry Pi</summary>
