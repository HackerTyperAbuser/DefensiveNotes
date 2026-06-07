# Playbook
- [ ] Knowing what application is installed on the system (some malware disguise with legit application names)
- [ ] Profile setup `imageinfo` `kdbgscan`
- [ ] Process with high level privilege
- [ ] Abnormal Names `pslist`
- [ ] Timestamp identification 
- [ ] "Singletons" process
	- wininit.exe
	- lsass.exe
	- services.exe
	- spoolsv.exe
- [ ] Parent child processes (`pstree`)
	- Path mismatch
	- Web browser spawning suspicious child process (mshta.exe)
	- Email client spawning suspicious child process (regsvr32.exe)
	- System process (services.exe) spawning client-side application process (calc.exe)
	- Windows explorer process (explorer.exe) spawning system process (lsass.exe)
- [ ] Processes running from unusual or unexpected locations
- [ ] Process with network activity: unusual times, a process that does not need connection, connection directions (Server to workstation, workstation to workstation -> lateral movement), low reputation IP Addresses.
- [ ] Hidden processes `psxview`
	- [ ] Process detail `psinfo`
	- [ ] Long and obfuscated command line arguments.
	- [ ] Process with network connections

| Extension | Description            |
| :-------- | ---------------------- |
| .vmdk     | Virutal disk image     |
| .vmem     | Virtual machine memory |
## System
(WinpMem) Dumping Windows Memory
```powershell
winpmem_mini_x64_rc2.exe memdump.raw
```
(Volatility) Identifying Profile
- Run this then KDBG scan to reduce scanning time
```bash
vol.py -f <MEMORY FILE> imageinfo
```
(Volatility) KDBG scan
- Note value of `Version64` and `Build string` -> update imageinfo profile
- Correct profile reveals more processes (`PsActiveProcessHead`)
- Use `kdCopyDataBlock` for `pslist` plugin
```cmd
vol.py -f <MEMORY FILE> --profile=Win7SP1x64 kdbgscan
```
## Processes
(Volatility) Identify Running Processes 
- `PPID`: parent process ID
- `Thds`: number of threads started
- `Hnds`: Handles to interact with objects like files, registry keys and other process. Number and type of handles opened by a process can analyze what resource the process accessed
- `Sess`: user logs onto Windows, a new session is created, this is user's session
- `Wow64`: 32-bit or 64-bit
```bash
vol.py -f <MEMORY FILE> --profile=Win7SP1x64 -g <kdCopyDatablock> pslist
```
(Volatility) Parent and child processes
```cmd
vol.py -f <MEMORY FILE> --profile=Win7SP1x64 pstree
```
(Volatility) Windows Running processes
```bash
vol.py -f <MEMORY FILE> --profile=Win7SP1x64 windows.pslist
```
(Volatility) Tree structure similar to Task Manager
```bash
vol.py -f <MEMORY FILE> --profile=Win7SP1x64 windows.pstree
```
Verbose
- `Audit`: Full PATH
- `cmd`: Command that was run
- `Path`: like the audit field, full path of the application on disk. Pstree uses two method to extract path as some malware can disguise by changing the Path https://www.ired.team/offensive-security/defense-evasion/masquerading-processes-in-userland-through-_peb. If there is a path mismatch IoC.
```cmd
vol.py -f <MEMORY FILE> --profile=Win7SP1x64 pstree -v
```
(Volatility) Parent and child processes (EPROCESS)
```bash
vol.py -f <MEMORY FILE> --profile=Win7SP1x64 psscan
```
(Volatility) Hidden processes
- `pslist` column similar to Task Manager, hidden process are good candidate for investigations
- Record address of suspicious process, useful for `psinfo`
```cmd 
vol.py -f <MEMORY FILE> --profile=Win7SP1x64 psxview
```
(Volatility) Examining process
- https://cysinfo.com/detecting-malicious-processes-psinfo-volatility-plugin/
```cmd
vol.py -f <MEMORY FILE> --profile=Win7SP1x64 psinfo -o <PROCESS ADDRESS>
```
(Volatility) Process privilege
- First SID is the SID that started the process
- `Mandatory Level`: Low, Medium, High (Administrators), System
```cmd 
vol.py -f <MEMORY FILE> --profile=Win7SP1x64 getsids -o <PROCESS ADDRESS>
```
![[Pasted image 20260510155958.png]]

## Network 
(Volatility) Identifying Network Artifacts (LISTENING & ESTABLISHED) -> similar to `netstat`
- Scan network pool tags: TcpL, TcpE and UdpA
- `UdpA`: UDP sockets
- `TcpL`: Listening TCP sockets
- `TcpE`: Established TCP sockets
- \[::\]:Port: Ipv6 address connection
- \[::1\]:Port: Ipv6 loopback address
- 0.0.0.0:Port: All interface
```bash
vol.py -f <MEMORY FILE> --profile=Win8SP1x64 -g <kdCopyDatablock> netscan
```
(Volatility) Network Artifacts (TERMINATED & ESTABLISHED)
```bash
vol.py -f <MEMORY FILE> --profile=Win8SP1x64 connscan
```
## $MFT
Viewing \$MFT entries
[[Master File Table]]
```cmd
vol.py -f <MEMORY FILE> --profile=Win8SP1x64 mftparser
```
![[Pasted image 20260510183815.png]]
## Services
(Volatility) Listing services
```bash
vol.py -f <MEMORY FILE> --profile=Win8SP1x64 svcscan
```
## Handles
(Volatility) File handles
```bash
vol.py -f <MEMORY FILE> --profile=Win8SP1x64 handles -p <PID> --object-type=File
```
(Volatility) Registry keys handles
```bash
vol.py -f <MEMORY FILE> --profile=Win8SP1x64 handles -p <PID> --object-type=Key
```
(Volatility) Process handles
```bash
vol.py -f <MEMORY FILE> --profile=Win8SP1x64 handles -p <PID> --object-type=Process
```
## Registry Hives
(Volatility) Registry
```bash
vol.py -f <MEMORY FILE> --profile=Win8SP1x64 hivelist
```
(Volatility) Reading registry keys
```cmd
vol.py -f <MEMORY FILE> --profile=Win8SP1x64 printkey -K <KEY>
```
## DLLs
(Volatility) Loaded DLLs for a PID
```bash
vol.py -f <MEMORY FILE> --profile=Win8SP1x64 dlllist -p <PID>
```

# Malware Artifacts Automation
## Injected code
(Volatility) Find potentially injected code (malware)
```bash
vol.py -f <MEMORY FILE> --profile=Win7SP1x64 malfind
```
## Persistence
Finding potential persistence related registry keys.
- User specific variants `HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run` or `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run`
- Persistence can be done on many keys.
```cmd
volatility -f <memory_dump> --profile=<profile> -g 0xf803788a44d8 winesap
```