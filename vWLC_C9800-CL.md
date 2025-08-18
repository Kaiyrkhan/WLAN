# Cisco vWLC (Virtual Wireless LAN Controller)

## Deploying the Cisco Catalyst 9800-CL on VMware ESXi

Software Download Link
https://software.cisco.com/download/home

> **Download File: C9800-CL-universalk9.17.15.03.ova**  
> Select a Product -> Browse all -> Wireless -> Wireless LAN Controller -> Standalone Controllers -> Catalyst 9800 Wireless Controllers for Cloud -> Catalyst 9800-CL Wireless Controller for Cloud -> IOS XE Software -> Cisco Catalyst 9800 Wireless Controller for Cloud - Hyper-V / ESXi / KVM -> download file: C9800-CL-universalk9.17.15.03.ova

**EdgeRT1**
```shell
ip nat inside source list NAT interface GigabitEthernet0/0/0 overload
ip access-list standard NAT
permit 10.0.128.0 0.0.0.255
permit 192.168.130.0 0.0.0.255
permit 192.168.150.0 0.0.0.255
```

**SRV-D1 Switch**
```shell
vlan 128
name vWLC-MGMT
vlan 130
name staff-WLAN
vlan 150
name student-WLAN

int vlan 128
ip address 10.0.128.251 255.255.255.0
no shutdown
int vlan 130
ip address 192.168.130.251 255.255.255.0
no shutdown
int vlan 150
ip address 192.168.150.251 255.255.255.0
no shutdown

ping 10.0.128.1
ping 192.168.130.1
ping 192.168.150.1

// Configure the Administrator User
username student privilege 15 secret class@123

// Configure the Wireless Management interface and Allow Management via Wireless 
wireless managemet interface vlan 128
exit
wireless mgmt-via-wireless

// Now we must temporarily disable the 2.4GHz, 5GHz, 6GHz bands
ap dot11 24ghz shutdown
ap dot11 5ghz shutdown
ap dot11 6ghz shutdown

// Configure the AP Country Code
ap country KZ

// Re-enable the bands
no ap dot11 5ghz shutdown
no ap dot11 24ghz shutdown
no ap dot11 6ghz shutdown

// Configure the WLC to sync time with an NTP server
ip route 0.0.0.0 0.0.0.0 10.0.128.1
ping ntp.nic.kz
ping 80.241.0.72
ntp server 80.241.0.72

// Generating the Self-Signed Certificate
SRV-D1# wireless config vwlc-ssc key-size 2048 signature-algo sha256 password 0 class@123

show wireless management trustpoint

copy run start
```
```shell
show wireless stats ap join summary
show ap tag summary
show ap uptime
show wlan summary
```

**Configure vWLC using Web UI**

Browser -> https://public_ip_address:44128

```shell
1-қадам: Monitoring -> Wireless -> AP Statistics
```

```shell
2-қадам: Configuration -> Layer2 -> VLAN
```

```shell
3-қадам: Configuration -> Tags & Profiles -> WLANs -> Add ->
General ->
- Profile Name: STAFF_WLAN
- SSID: staff-WiFi
- Status: Enabled
- 6 GHz Status: Disabled

Security -> Layer2 -> Auth Key Mgmt (AKM) -> PSK -> Pre-Shared Key: staff@123
Apply to Device
```

```shell
4-қадам: Configuration -> Tags & Profiles -> Policy -> Add -> 

General ->
- Name: POLICY_PROFILE_STAFF
- Description: POLICY PROFILE STAFF
- Status: Enabled

Access Policies -> VLAN/VLAN Group: staff-WiFi
Apply to Device
```

```shell
5-қадам: 
```

```shell
6-қадам: 
```

```shell
```
```shell
```

## References
1) [Cisco Catalyst 9800-CL Wireless Controller for Cloud Deployment Guide](https://www.cisco.com/c/en/us/td/docs/wireless/controller/9800/technical-reference/c9800-cl-dg.html)
2) [Understand Catalyst 9800 Wireless Controllers Configuration Model](https://www.cisco.com/c/en/us/support/docs/wireless/catalyst-9800-series-wireless-controllers/213911-understand-catalyst-9800-wireless-contro.html)
3) [Deploying and Configuring the Cisco Catalyst 9800-CL in VMware ESXi](https://www.wifireference.com/2019/08/24/cisco-catalyst-9800-cl-deployment-guide/)

## YouTube
1) [Install Cisco C9800-CL in VMWare ESXI 7 | Joining AP](https://youtu.be/mI6q8pkXKZI)
2) [Install Cisco Wireless LAN Controller C9800-CL | Joining AP](https://youtu.be/ef4amrMiyaY)
3) [Cisco 9800 VMware ESXi install](https://youtu.be/S4qYimtm2mQ)
4) [Deploying the Cisco Catalyst 9800-CL in VMware ESXi](https://youtu.be/DqqjF2FH_Zw)
