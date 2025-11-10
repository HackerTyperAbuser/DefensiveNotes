OpenSSH config file: `/etc/ssh/sshd_config`
- Always restart the service after configuration!

- [ ] Disabling root login on SSH.
```
PermitRootLogin no
```
- [ ] Prevent root account from being log in  
```bash
sudo useradd -m -c "New Admin" newadmin
sudo passwd newadmin
sudo usermod -aG sudo newadmin # add to SUDO group

# Change to nologin shell method
sudo nano /etc/passwd # change /bin/bash -> /usr/sbin/nologin
```
### Key management
- [ ] Key authentication instead of password
	- Always use a passphrase
```bash
ssh-keygen -t rsa
ssh-copy-id <USER>@<SERVER>

# Config file
PasswordAuthentication no
```
