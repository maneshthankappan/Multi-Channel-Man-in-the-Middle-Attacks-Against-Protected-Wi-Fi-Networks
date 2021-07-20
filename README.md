# Multi Channel Man-in-the-Middle Attacks Against Protected Wi-Fi Networks
This activity describes how to perform MC-MitM (Improved Variant) attack using channel switch announcements.To execute this attack, two important the packeges such as python2.7 and scapy 2.3.3 are required.Note that this attack will not be successful with latest scapy versions 2.4.3. In this case it is advisble to remove higher versions of scapy and then downgrade to 2.3.3. In particular, this MC-MitM attack ultimately peforms a key reinstalltion attack on Linux machine. More specifically, the all-zero encryption key attack on vulnerable wpa_supplicants (2.4 or below) that comes with various Linux distributions. Please, use [this tool](https://github.com/lucascouto/krackattacks-scripts) to verify the client is vunarable to the attack or not. 
## Brief Background  
Under Construction
## Attack Environment Setup
This tool is tested with the following equipaments:

* Attacker Machine
  * HP Elite 8300 SFF Quad Core
  * OS: Kali Linux 2019.4(5.3.0-kali2-amd64)
  * Two Wi-Fi Cards: Qualcomm Atheros Communications AR9271. Driver: ath9k_htc
  * Android smartphone connected via usb to provide 4g Internet

* Client Aor Victim Machine:
  * Dell Inspiron 15 30000 series
  * OS: Ubuntu 17.04
  * wpa_supplicant v2.4 (2.4-0ubuntu6 am64)

* Access Point:
  * D-Link AX 1500 Wi-Fi 6 Router
  * Hardware Version: A2
  * Firmware Version: 1.08
  * Configured with 50% TX power and channel 1
  
## Prerequisites and Installation Procedure
### 1. Install the following dependencies on Kali Linux:
```
$sudo apt update
$sudo apt install libnl-3-dev libnl-genl-3-dev pkg-config libssl-dev net-tools git sysfsutils python-pycryptodome
```
### 2. Install the following scapy package
```
$ pip install scapy==2.3.3
```
If the above command gives error, please try following procedure to install scapy 2.3.3
```
1. Go to https://pypi.org/project/scapy/2.3.3/#files
2. Download "scapy-2.3.3.tgz (1.4 MB)" folder
3. Unzip/extract the folder
4. Open a terminal in scapy-2.3.3 folder
5. Type sudo python2.7 setup.py install
```
### 3. Install the following python package for MC-MitM attack setup
```
$pip install --user mitm_channel_based
```
If the above command gives error, please try following procedure to install MC-MitM package
```
1. Go to https://pypi.org/project/mitm-channel-based/#description
2. Click on "Download files" link
3. Download "mitm_channel_based-0.0.5.tar.gz (11.7 kB)" file
4. Go to your download folder and unzip the above folder
5. Open a terminal in "mitm_channel_based-0.0.5" folder
6. Type sudo python2.7 setup.py install
```
### 4. Warnings
Perform the following before executing the attack
```
1. Goto "krackattack-all-zero-tk-key-master" folder
2. Execute the script "./disable-hwcrypto.sh" to disable hardware encryption
3. Reboot the system
4. Verify whether the flag (nohwcrypt = "1") has been set using the command "systool -vm ath9k_htc"
5. Disable Wi-Fi or type sudo nmcli radio wifi
6. Type suso rfkill unblock wifi
```
## Tool Usage
 The attack tool can be executed using follwoing command line arguments. Download attack folder from the link (Under construction). 

 ```
 $sudo ./krack_all_zero_tk.py wlan1 wlan0 eth0 "Manesh_WiFi" -t e4:02:9b:cd:3b:92
 ```
 ### Below are the details of wireless interfaces
 
 * `wlan1`: interface that listens and injects packets on the real channel
 * `wlan0`: interface that runs the Rogue AP
 * `eth0`: interface in which is provided internet access
 * `"Manesh_WiFi"`: SSID of the target network
 * `-t e4:02:9b:cd:3b:92`: MAC address of the attacked client
 * You can see many other options running `./krackattack/krack_all_zero_tk.py -h`!
 

 ### Files Generated
 After running the script for the first time, some new files will be generated:
 ```
 * `dnsmasq.conf`: configuration file for DHCP and DNS services
 * `dnsmasq_log`: output from dnsmasq
 * `hostapd_rogue.conf`: configuration file for the rogue ap clone from the real ap
 * `hostapd_rogue.log`: output from hostapd_rogue
 * `rogue_ap_capture.pcap`: file containing packets capture from the rogue ap interface
 ```
  ## Demonstration Video
[![Analysis of Network behavior during channel switch announcements](https://github.com/maneshthankappan/Multi-Channel-Man-in-the-Middle-Attacks-Against-Protected-Wi-Fi-Networks/blob/main/thumb.jpg)](https://www.youtube.com/watch?v=axqbioyjom0)

  ## Analysis of network behavior during MC-MitM attack
  Under construction  
  
  ## Troubleshooting
  Under construction  
 
  ### References
