- Acquisition tool should be on a USB never installed on the host system.
- Extracted to the USB.
# Windows
DumpIt
- [ ] Dump to USB drive (> size than victim system RAM)
- [ ] Validate corruption
```cmd
DumpIt.exe
volatility -f <MEMORY> imageinfo
```
## Dead Systems
- Hibernation file (`C:\hiberfil.sys`): Use to restore the session when machine is repowered, size =< RAM size
- Paging file (`C:\pagefile.sys`): Temp file to move infrequent RAM memory to hard disk.
- Crash Dumps (`C:\Windows\MEMORY.DMP`): BSOD dump log
![[Pasted image 20260510001545.png]]
# Linux
Acquire Linux Kernel verison
```bash
uname -a
```