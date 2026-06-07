- [ ] Statistics: Capture File Properties
- [ ] Check IP Reputation: https://www.abuseipdb.com/ || https://www.ipqualityscore.com/
- [ ] Statistics: Protocol Hierarchy
- [ ] Statistics: All Addresses
- [ ] Statistics: Destination and Ports
- [ ] Filtering and following protocol streams
- [ ] Extracted Files: VirusTotal || AnyRun
# Filters
Common filters
```
ip.addr == 192.168.1.1
ip.src == 192.168.1.1
ip.dst == 192.168.1.1
ip.addr = 192.168.1.1 && ip.addr == 10.0.0.1
dns
tcp 
udp
http
http.request
http.host == "exmaple.com"
http.request.url == "/login"
http.request.method == "POST"
arp
tcp.flags.reset == 1
tcp.analysis.retransmission
tcp.flags.syn == 1 or tcp.flags.fin == 1
tcp.stream eq X
tcp.port == 443
udp.port == 53
tcp.port in {80, 443}
frame contians "password"
!(arp or icp or dns)
```
# File Extraction
File > Export Objects > HTTP (or other relevant protocol)
![[Pasted image 20260510150104.png]]
Binwalk on extracted files
```bash
binwalk <FILE>
binwalk -e <FILE>
```