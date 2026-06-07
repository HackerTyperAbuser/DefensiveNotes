[[Master File Table]]
# Playbook
- Stored under `C:\$MFT`
- \[root\] folder in FTK Imager
- Tools: R-studio, MFTEcmd + Timeline Explorer, NTFS Log Tracker
```cmd
MFTECmd.exe -f "C:\$MFT" --csv "C:\Users\IEUser\Desktop" --csvf mft_output.csv
```
![[Pasted image 20260520010555.png]]
## Timeline Explorer
![[Pasted image 20260520005504.png]]
1. Entry Number: cross reference records between $MFT and $USNJRNL
2. Parent Entry Number: parent folder where file resides
3. In use: if uncheck, it's deleted. The value "Last record Change" column will indicate when object was deleted.
4. Parent Path: location of file
5. File name
6. File Extension
7. Is directory: if checked object is a folder if not it is a file
8. Has Ads: object contains Alternate Data Streams
9. Is Ads: each file can have multiple streams. Each stream will have its record in $MFT.
10. File size: if record belongs to a folder, size will be 0
11. Created0x10: creation date