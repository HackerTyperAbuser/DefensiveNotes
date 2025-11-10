- [ ] SELinux
- [ ] Fail2ban IPS protects against brute-force attacks

- [ ] Check for updates
```bash
sudo apt update
sudo apt upgrade
```
- [ ] Remove unnecessary packages of outdated services
```bash
sudo apt --purge remove xinetd nis yp-tools tftpd atftpd tftpd-hpa telnetd rsh-server rsh-redone-server
```
(dpkg) All installed packages
```bash
sudo dpkg --list
```
## Services
(systemctl) All services and states
- enabled: start at bootup
- disabled: won't start at bootup but can start manually
- masked: won't start at bootup & cannot start manually
- static: cannot be enabled, one time use.
```bash
sudo systemctl list-unit-files --type=service
```
(systemctl) Service states
```bash
sudo systemctl status <SERVICE>
sudo systemctl stop <SERVICES>
sudo systemctl start <SERVICES>
```
## Firewalls
- Iptables are reset after every reboot -> need to make it persistent rules

(iptables) Firewall rules
```bash
sudo iptables -L
```
(iptables) Setting up firewall rules (accepting HTTP traffic anywhere)
```bash
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT
```
