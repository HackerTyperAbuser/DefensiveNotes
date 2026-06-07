![[Pasted image 20260520013725.png]]
File may still exists in Windows Search Database despite being deleted. The database also captures user interactions to Microsoft Edge, Internet Explorer
- `C:\ProgramData\Microsoft\Search\Data\Applications\Windows\Windows.edb`
- Windows 11: `C:\ProgramData\Microsoft\Search\Data\Applications\Windows\Windows.db`
- Tool: Search Index Database Reporter (SIDR) + Timeline Explorer
```cmd
sidr.exe <PATH_TO_WINDOWS_DB> -o C:\Users\<user>\Desktop\Output -f csv
```
![[Pasted image 20260520014052.png]]
