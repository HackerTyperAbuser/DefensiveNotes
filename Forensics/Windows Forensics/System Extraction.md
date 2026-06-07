# Windows
## System Information
Extracting Windows version
```cmd
SOFTWARE\Microsoft\Windows NT\CurrentVersion
// or
winever.exe
```
**Computer name**
- Check Security Event Log
![[Pasted image 20260510014441.png]]
```cmd
System\ControlSet001\Control\ComputerName\ComputerName
```
**Time zone**
- Registry use UTC & Event Log use machine's local time
- 'Bias' key to find time zone set on machine
```cmd
SYSTEM\ControlSet001\Control\TimeZoneInformation
```
**Shut down & Startup**
- Encoded using Windows FILETIME timestamp
- Event log 1074, 6005 and 6006
- Unexpected shutdown: 6008, 41
```cmd
System\ControlSet001\Control\Windows
```
## Network 
- `EnableDhcp` -> IP assigned by DHCP
- `DhcpIPAddress` -> IPv4 address given by DHCP
- `LeaseObtainedTime` -> Time when DHCP assigned IP address
- `DhcpNetworkHint` -> Previously connected wireless network (HEX format)
```cmd
SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkCards //Physical
\SYSTEM\ControlSet001\Services\Tcpip\Parameters\Interfaces //All
```
**Previous connections**
- http://wigle.net/ - SSID and MAC to find geolocation of network
- `NameType`: 0x47 wireless, 0x6 wired, 0x17 broadband connections
- `DefaultGatewayMac`: MAC address
- `Description` & `FirstNetwork`: SSID
- Event ID 8001 successful connection
- Event ID 8003 successful disconnection
- [[Windows Event Log#Parsing Wi-Fi Connections]]
```cmd
SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Signatures\Unmanaged
HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Profiles
Microsoft-Windows-WLAN-AutoConfig%4Operational.evtx // connection time event log
```
**Network Shares**
- `Path`: local path of shared object
- `Permission`: how share was created '0' simple sharing GUI, '9' advanced sharing GUI, '63' command line
- `ShareName`: name of share on network
- `Type`: '0' drive or folder, '1' printer, '2' device
```cmd
SYSTEM\ControlSet001\Services\LanmanServer\Shares
```
## User
SAM (https://github.com/keydet89/RegRipper3.0):
- `C:\Windows\System32\config\SAM`
- `C:\Windows\Repair\SAM`
## Files
- C:\Windows\Temp
- C:\Users\<user>\Desktop
- C:\Users\<user>\Documents
- C:\Users\<user>\Downloads
- C:\Users\<user>\Appdata
- C:\Windows\System32