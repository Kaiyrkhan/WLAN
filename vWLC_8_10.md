# Cisco vWLC (Virtual Wireless LAN Controller)

Software Download Link
https://software.cisco.com/download/home

> **Download file: AIR_CTVM-K9_8_10_196_0.ova**  
> Select a Product -> Browse all -> Wireless -> Wireless LAN Controller -> Standalone Controllers -> Virtual Wireless Controller -> Wireless LAN Controller Software -> Cisco Wireless LAN Small Scale Virtual Controller Installation with 60 day evaluation license (AIR_CTVM-K9_8_10_196_0.ova) -> download

**vWLC**
```shell
Would you like to terminate autoinstall? [yes]: yes

System Name [Cisco_xx:xx:xx] (31 characters max): vWLC1

Enter Administrative User Name (24 characters max): admin
Enter Administrative Password (3 to 127 characters): admin@123

Enter User Name for AP (24 characters max): student
Enter Password for AP (6 to 127 characters): student@123

Enter Enable Password for AP (6 to 127 characters): class@123

Service Interface IP Address Configuration [statis][DHCP]: DHCP

Management Interface IP Address: 10.0.128.251
Management Interface Netmask: 255.255.255.0
Management Interface Default Router: 10.0.128.1
Management Interface VLAN Identifier (0 = untagged): 128
Management Interface Port Num [1]: 1
Management Interface DHCP Server IP Address: 10.0.128.1

Virtual Gateway IP Address: 192.0.2.1
Mobility/RF Group Name: default

Network Name (SSID): staff-WiFi
Configure DHCP Bridging Mode [yes][NO]: no
Allow Static IP Addresses [YES][no]: yes
Configure a RADIUS Server now? [YES][no]: no
Enter Country Code list (enter ‘help’ for a list of countries) [US]: help
Enter Country Code list (enter ‘help’ for a list of countries) [US]: KZ

Enable 802.11b Network [YES][no]: yes
Enable 802.11a Network [YES][no]: yes
Enable 802.11g Network [YES][no]: yes
Enable Auto-RF [YES][no]: yes

Configure a NTP server now? [YES][no]: yes
Enter the NTP server's IP address: 80.241.0.72
Enter a polling interval between 3600 and 604800 secs: 86400

Would you like to configure IPv6 parameters [YES][no]: no

Configuration correct? If yes, system will save it and reset. [yes][NO]: yes

User: admin
Password: admin@123
Cisco Controller> show interface summmary

Browser -> httрs://10.0.128.251
```
