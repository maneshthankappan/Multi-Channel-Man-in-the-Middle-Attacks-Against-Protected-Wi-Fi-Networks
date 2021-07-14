# Multi Channel Man-in-the-Middle Attacks Against Protected Wi-Fi Networks
This activity describes how to perform MC-MitM (Improved Variant) attack using channel switch announcements.To execute this attack, two important the packeges such as python2.7 and scapy 2.3.3 are required.Note that this attack will not be successful with latest scapy versions 2.4.3. In this case it is advisble to remove higher versions of scapy and then downgrade to 2.3.3. In particular, this MC-MitM attack ultimately peforms a key reinstalltion attack on Linux machine. More specifically, the all-zero encryption key attack on vulnerable wpa_supplicants (2.4 or below) that comes with various Linux distributions. Please, use [this tool](https://github.com/lucascouto/krackattacks-scripts) to verify the client is vunarable to the attack or not. 
## Brief Background  
Hostapd (host access point daemon) is a user space daemon software enabling a network or wireless interface card to act as an access point and authentication server. 
hostapd_cli is a frontend program to interact with hostapd. It is used to query the status of hostapd and set parameters through command line interface.In this activity, hostapd_cli is used to send channel switch command over the control interface on which hostapd is running. Following are the detailed steps.
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
