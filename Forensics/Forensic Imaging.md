
| Extension | Description            |
| :-------- | ---------------------- |
| .vmdk     | Virutal disk image     |
| .vmem     | Virtual machine memory |
(WinpMem) Dumping Windows Memory
```powershell
winpmem_mini_x64_rc2.exe memdump.raw
```
(Volatility) Identifying Profile
```bash
vol.py -f <MEMORY FILE> imageinfo
```
## Processes
(Volatility) Identify Running Processes 
```bash
vol.py -f <MEMORY FILE> --profile=Win7SP1x64 pslist
```
(Volatility) Parent and child processes (EPROCESS)
```bash
vol.py -f <MEMORY FILE> --profile=Win7SP1x64 psscan
```
(Volatility) Windows Running processes
```bash
vol.py -f <MEMORY FILE> --profile=Win7SP1x64 windows.pslist
```
(Volatility) Tree structure similar to Task Manager
```bash
vol.py -f <MEMORY FILE> --profile=Win7SP1x64 windows.pstree
```
## Network 
(Volatility) Identifying Network Artifacts (LISTENING & ESTABLISHED)
```bash
vol.py -f <MEMORY FILE> --profile=Win8SP1x64 netscan
```
(Volatility) Network Artifacts (TERMINATED & ESTABLISHED)
```bash
vol.py -f <MEMORY FILE> --profile=Win8SP1x64 connscan
```
## Injected code
(Volatility) Find potentially injected code (malware)
```bash
vol.py -f <MEMORY FILE> --profile=Win7SP1x64 malfind
```
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
## DLLs
(Volatility) Loaded DLLs for a PID
```bash
vol.py -f <MEMORY FILE> --profile=Win8SP1x64 dlllist -p <PID>
```